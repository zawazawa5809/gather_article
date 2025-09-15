# PySide6 テーマ設計包括的ガイドライン

## 調査概要

- 調査日時: 2025-09-15T10:00:00+09:00
- 検索範囲: jp/en/both / 深度: detailed / 期間: 2024-2025
- 検索手段: web.search (複数クエリによる段階的調査)
- 参照ガイド: guide.md (Knowledge Management System テーマ実装ガイド)

## 主要な発見事項

### 1. 定義/仕様

- **QPaletteベース設計** [1][2]: PySide6のテーマシステムの基盤として、QPaletteによる色役割管理が最も推奨される
- **QStyleSheet (QSS)** [3]: CSS-likeな記法で詳細なスタイリングが可能、palette()参照による動的テーマ対応
- **Fusionスタイル** [1][4]: クロスプラットフォーム対応とダークモード実装において必須
- **プラグインアーキテクチャ** [5]: カスタムウィジェットの再利用とモジュール化を実現

### 2. 公式発表

- **Qt for Python 6.9.2** [6]: 2024年時点での最新安定版、パフォーマンス改善とバグ修正を含む
- **pytest-qt** [7]: PySide6アプリケーションの自動テストフレームワーク
- **FluentWinUI3スタイル** [8]: Qt Quick Controls向けの新スタイル統合

## 詳細情報

### セクション A: コアアーキテクチャ設計

#### 1. 階層型テーマシステム

```python
# テーマアーキテクチャの層構造
"""
┌─────────────────────────────────────┐
│     アプリケーションレベル           │
│  (ThemeManager, 設定, 永続化)        │
├─────────────────────────────────────┤
│     コンポーネントレベル             │
│  (カスタムウィジェット, スタイル)    │
├─────────────────────────────────────┤
│     システムレベル                   │
│  (QPalette, QStyle, QStyleSheet)     │
└─────────────────────────────────────┘
"""
```

#### 2. テーママネージャー実装パターン

```python
from PySide6.QtWidgets import QApplication
from PySide6.QtGui import QPalette, QColor
from PySide6.QtCore import QObject, Signal
from typing import Dict, Optional
import json
from pathlib import Path

class ThemeManager(QObject):
    """統一されたテーマ管理システム"""

    theme_changed = Signal(str)  # テーマ変更シグナル

    def __init__(self, app: QApplication):
        super().__init__()
        self.app = app
        self.themes: Dict[str, Dict] = {}
        self.current_theme: Optional[str] = None
        self._load_theme_definitions()

    def _load_theme_definitions(self):
        """テーマ定義をJSONから読み込み"""
        theme_dir = Path("themes")
        for theme_file in theme_dir.glob("*.json"):
            with open(theme_file, 'r', encoding='utf-8') as f:
                theme_data = json.load(f)
                self.themes[theme_file.stem] = theme_data

    def apply_theme(self, theme_name: str):
        """テーマを適用"""
        if theme_name not in self.themes:
            raise ValueError(f"Unknown theme: {theme_name}")

        # Fusionスタイルを強制（必須）
        self.app.setStyle("Fusion")

        # パレット生成と適用
        palette = self._create_palette(self.themes[theme_name])
        self.app.setPalette(palette)

        # グローバルスタイルシート適用
        qss = self._generate_qss(self.themes[theme_name])
        self.app.setStyleSheet(qss)

        # すべてのウィジェットを再描画
        self._repolish_widgets()

        self.current_theme = theme_name
        self.theme_changed.emit(theme_name)

    def _create_palette(self, theme: Dict) -> QPalette:
        """テーマ定義からQPaletteを生成"""
        palette = QPalette()

        # 色役割マッピング
        color_roles = {
            'window': QPalette.Window,
            'window_text': QPalette.WindowText,
            'base': QPalette.Base,
            'alternate_base': QPalette.AlternateBase,
            'text': QPalette.Text,
            'button': QPalette.Button,
            'button_text': QPalette.ButtonText,
            'highlight': QPalette.Highlight,
            'highlighted_text': QPalette.HighlightedText,
            'mid': QPalette.Mid,
            'shadow': QPalette.Shadow,
            'light': QPalette.Light,
            'disabled_text': QPalette.PlaceholderText
        }

        colors = theme.get('colors', {})
        for key, role in color_roles.items():
            if key in colors:
                palette.setColor(role, QColor(colors[key]))

        return palette

    def _generate_qss(self, theme: Dict) -> str:
        """テーマ定義からQSSを生成"""
        qss_parts = []

        # 基本スタイル
        qss_parts.append("""
        * {
            font-family: '%(font_family)s';
            font-size: %(font_size)spx;
        }

        QWidget {
            background-color: palette(window);
            color: palette(window-text);
        }

        /* 入力フィールド標準スタイル */
        QLineEdit, QTextEdit, QPlainTextEdit {
            background-color: palette(base);
            color: palette(text);
            border: 1px solid palette(mid);
            border-radius: %(border_radius)spx;
            padding: %(padding)spx;
        }

        QLineEdit:focus, QTextEdit:focus, QPlainTextEdit:focus {
            border-color: palette(highlight);
            border-width: 2px;
        }

        /* ボタン標準スタイル */
        QPushButton {
            background-color: palette(button);
            color: palette(button-text);
            border: 1px solid palette(mid);
            border-radius: %(border_radius)spx;
            padding: %(padding)spx %(padding_large)spx;
            min-height: %(min_button_height)spx;
        }

        QPushButton:hover {
            background-color: palette(light);
        }

        QPushButton:pressed {
            background-color: palette(shadow);
        }

        QPushButton:disabled {
            color: palette(disabled-text);
            background-color: palette(window);
        }
        """ % theme.get('dimensions', {
            'font_family': 'Segoe UI',
            'font_size': 10,
            'border_radius': 4,
            'padding': 6,
            'padding_large': 12,
            'min_button_height': 24
        }))

        # カスタムスタイル追加
        if 'custom_qss' in theme:
            qss_parts.append(theme['custom_qss'])

        return '\n'.join(qss_parts)

    def _repolish_widgets(self):
        """すべてのウィジェットのスタイルを再適用"""
        for widget in self.app.allWidgets():
            widget.style().unpolish(widget)
            widget.style().polish(widget)
            widget.update()
```

### セクション B: デザイントークンシステム

#### 1. トークン定義構造

```json
{
  "name": "dark_professional",
  "version": "1.0.0",
  "colors": {
    "window": "#232428",
    "window_text": "#eeeeee",
    "base": "#2b2d31",
    "alternate_base": "#33353a",
    "text": "#eeeeee",
    "button": "#2b2d31",
    "button_text": "#eeeeee",
    "highlight": "#2f6fff",
    "highlighted_text": "#ffffff",
    "mid": "#45474c",
    "shadow": "#121315",
    "light": "#58595e",
    "disabled_text": "#808080",

    "semantic": {
      "error": "#ff5252",
      "warning": "#ffb74d",
      "success": "#4caf50",
      "info": "#2196f3"
    }
  },
  "dimensions": {
    "font_family": "Segoe UI",
    "font_size": 10,
    "font_size_large": 12,
    "font_size_small": 9,
    "line_height": 1.5,
    "border_radius": 4,
    "border_radius_large": 8,
    "padding": 6,
    "padding_large": 12,
    "spacing": 8,
    "min_button_height": 24,
    "icon_size": 16,
    "icon_size_large": 24
  },
  "animations": {
    "duration_fast": 150,
    "duration_normal": 250,
    "duration_slow": 400,
    "easing": "ease-in-out"
  }
}
```

#### 2. トークン使用ガイドライン

```python
class ThemedWidget(QWidget):
    """テーマ対応カスタムウィジェット基底クラス"""

    def __init__(self, parent=None):
        super().__init__(parent)
        self.theme_manager = self.get_theme_manager()
        self.theme_manager.theme_changed.connect(self.on_theme_changed)

    def get_theme_manager(self) -> ThemeManager:
        """アプリケーションのThemeManagerインスタンスを取得"""
        app = QApplication.instance()
        return getattr(app, 'theme_manager', None)

    def on_theme_changed(self, theme_name: str):
        """テーマ変更時の処理"""
        self.update_styles()
        self.update()

    def update_styles(self):
        """スタイルを更新（サブクラスでオーバーライド）"""
        pass

    def paintEvent(self, event):
        """palette()を使用した描画"""
        from PySide6.QtGui import QPainter
        painter = QPainter(self)
        palette = self.palette()

        # 常にパレットから色を取得
        painter.fillRect(self.rect(), palette.color(QPalette.Window))
        painter.setPen(palette.color(QPalette.WindowText))
        # ... 描画処理
```

### セクション C: コンポーネント設計パターン

#### 1. ファクトリーパターンによるウィジェット生成

```python
class WidgetFactory:
    """統一されたスタイルでウィジェットを生成"""

    @staticmethod
    def create_button(text: str, button_type: str = "default") -> QPushButton:
        button = QPushButton(text)

        # タイプ別スタイルクラス適用
        style_classes = {
            "default": "",
            "primary": "primary-button",
            "danger": "danger-button",
            "success": "success-button"
        }

        if button_type in style_classes:
            button.setProperty("class", style_classes[button_type])

        return button

    @staticmethod
    def create_input_field(placeholder: str = "", validator=None) -> QLineEdit:
        field = QLineEdit()
        field.setPlaceholderText(placeholder)

        if validator:
            field.setValidator(validator)

        # 統一されたスタイル適用
        field.setProperty("class", "themed-input")

        return field

    @staticmethod
    def create_card_widget(title: str, content: QWidget) -> QWidget:
        """カード型コンテナウィジェット"""
        card = QWidget()
        card.setProperty("class", "card-widget")

        layout = QVBoxLayout(card)

        # タイトル
        title_label = QLabel(title)
        title_label.setProperty("class", "card-title")
        layout.addWidget(title_label)

        # セパレータ
        separator = QFrame()
        separator.setFrameShape(QFrame.HLine)
        separator.setProperty("class", "card-separator")
        layout.addWidget(separator)

        # コンテンツ
        layout.addWidget(content)

        return card
```

#### 2. コンポジションパターンによる複合ウィジェット

```python
class SearchBar(ThemedWidget):
    """テーマ対応検索バーコンポーネント"""

    search_triggered = Signal(str)

    def __init__(self, parent=None):
        super().__init__(parent)
        self._setup_ui()

    def _setup_ui(self):
        layout = QHBoxLayout(self)
        layout.setContentsMargins(0, 0, 0, 0)

        # 検索アイコン
        self.icon_label = QLabel()
        self.icon_label.setProperty("class", "search-icon")
        layout.addWidget(self.icon_label)

        # 入力フィールド
        self.search_input = QLineEdit()
        self.search_input.setPlaceholderText("検索...")
        self.search_input.setProperty("class", "search-input")
        self.search_input.returnPressed.connect(self._on_search)
        layout.addWidget(self.search_input)

        # クリアボタン
        self.clear_button = QPushButton("×")
        self.clear_button.setProperty("class", "clear-button")
        self.clear_button.clicked.connect(self.search_input.clear)
        self.clear_button.setVisible(False)
        layout.addWidget(self.clear_button)

        # 入力監視
        self.search_input.textChanged.connect(self._on_text_changed)

    def _on_text_changed(self, text: str):
        self.clear_button.setVisible(bool(text))

    def _on_search(self):
        self.search_triggered.emit(self.search_input.text())

    def update_styles(self):
        """テーマ変更時のアイコン更新"""
        theme_manager = self.get_theme_manager()
        if theme_manager and theme_manager.current_theme:
            icon_path = f"icons/{theme_manager.current_theme}/search.svg"
            if Path(icon_path).exists():
                pixmap = QPixmap(icon_path)
                self.icon_label.setPixmap(pixmap.scaled(16, 16))
```

### セクション D: 統一性維持のためのガイドライン

#### 1. コーディング規約

##### 必須ルール

```python
# ✅ 良い例: palette()参照を使用
widget.setStyleSheet("""
    QWidget {
        background-color: palette(window);
        color: palette(window-text);
        border: 1px solid palette(mid);
    }
""")

# ❌ 悪い例: 直接色指定
widget.setStyleSheet("""
    QWidget {
        background-color: #232428;  # 絶対に避ける
        color: white;               # 絶対に避ける
    }
""")
```

##### 命名規則

```python
# ウィジェットプロパティ命名
widget.setProperty("role", "primary")      # 役割
widget.setProperty("state", "active")      # 状態
widget.setProperty("variant", "compact")   # バリアント
widget.setProperty("class", "card-widget") # クラス

# スタイルクラス命名（BEM風）
# ブロック__エレメント--モディファイア
"search-bar"              # ブロック
"search-bar__input"       # エレメント
"search-bar__input--error" # モディファイア付き
```

#### 2. 機能追加時のチェックリスト

```markdown
## 新機能実装チェックリスト

### 設計フェーズ
- [ ] 既存のデザイントークンで実装可能か確認
- [ ] 新しい色が必要な場合、セマンティックカラーから選択
- [ ] カスタムウィジェットはThemedWidget基底クラスを継承
- [ ] WidgetFactoryの利用を検討

### 実装フェーズ
- [ ] palette()参照のみを使用（直接色指定禁止）
- [ ] Fusionスタイルでの動作確認
- [ ] プロパティによるスタイルクラス設定
- [ ] テーマ変更シグナルへの対応

### テストフェーズ
- [ ] ライトテーマでの表示確認
- [ ] ダークテーマでの表示確認
- [ ] テーマ切り替え時の再描画確認
- [ ] 無効状態での表示確認
- [ ] HiDPI環境での表示確認

### ドキュメント
- [ ] コンポーネントカタログへの追加
- [ ] スタイルガイドの更新
- [ ] 使用例の作成
```

#### 3. コンポーネントカタログ

```python
class ComponentCatalog(QMainWindow):
    """全コンポーネントのショーケース"""

    def __init__(self):
        super().__init__()
        self.setWindowTitle("コンポーネントカタログ")
        self._setup_ui()

    def _setup_ui(self):
        central = QWidget()
        self.setCentralWidget(central)

        scroll = QScrollArea()
        scroll.setWidgetResizable(True)

        container = QWidget()
        layout = QVBoxLayout(container)

        # 各コンポーネントのデモ
        self._add_buttons_section(layout)
        self._add_inputs_section(layout)
        self._add_cards_section(layout)
        self._add_tables_section(layout)

        scroll.setWidget(container)
        main_layout = QVBoxLayout(central)
        main_layout.addWidget(scroll)

    def _add_buttons_section(self, layout):
        section = self._create_section("ボタン")

        buttons_layout = QHBoxLayout()
        buttons_layout.addWidget(WidgetFactory.create_button("デフォルト", "default"))
        buttons_layout.addWidget(WidgetFactory.create_button("プライマリ", "primary"))
        buttons_layout.addWidget(WidgetFactory.create_button("危険", "danger"))
        buttons_layout.addWidget(WidgetFactory.create_button("成功", "success"))

        disabled = WidgetFactory.create_button("無効", "default")
        disabled.setEnabled(False)
        buttons_layout.addWidget(disabled)

        section.layout().addLayout(buttons_layout)
        layout.addWidget(section)
```

### セクション E: パフォーマンスとアクセシビリティ

#### 1. パフォーマンス最適化

```python
class LazyStyleLoader:
    """遅延スタイル読み込み"""

    _cache = {}

    @classmethod
    def load_style(cls, style_name: str) -> str:
        if style_name not in cls._cache:
            style_path = Path(f"styles/{style_name}.qss")
            if style_path.exists():
                with open(style_path, 'r', encoding='utf-8') as f:
                    cls._cache[style_name] = f.read()
            else:
                cls._cache[style_name] = ""
        return cls._cache[style_name]

    @classmethod
    def clear_cache(cls):
        cls._cache.clear()
```

#### 2. アクセシビリティ対応

```python
def ensure_accessibility(widget: QWidget):
    """アクセシビリティ設定の確保"""

    # コントラスト比の確認
    palette = widget.palette()
    bg_color = palette.color(QPalette.Window)
    fg_color = palette.color(QPalette.WindowText)

    contrast_ratio = calculate_contrast_ratio(bg_color, fg_color)
    if contrast_ratio < 4.5:
        logging.warning(f"Low contrast ratio: {contrast_ratio}")

    # アクセシビリティ属性の設定
    if isinstance(widget, QPushButton):
        if not widget.accessibleName():
            widget.setAccessibleName(widget.text())
        widget.setAccessibleDescription(f"ボタン: {widget.text()}")

    elif isinstance(widget, QLineEdit):
        if widget.placeholderText():
            widget.setAccessibleDescription(widget.placeholderText())

def calculate_contrast_ratio(color1: QColor, color2: QColor) -> float:
    """WCAG 2.1準拠のコントラスト比計算"""
    def relative_luminance(color: QColor) -> float:
        def adjust(val):
            val = val / 255.0
            return val / 12.92 if val <= 0.03928 else ((val + 0.055) / 1.055) ** 2.4

        r, g, b = adjust(color.red()), adjust(color.green()), adjust(color.blue())
        return 0.2126 * r + 0.7152 * g + 0.0722 * b

    l1 = relative_luminance(color1)
    l2 = relative_luminance(color2)

    lighter = max(l1, l2)
    darker = min(l1, l2)

    return (lighter + 0.05) / (darker + 0.05)
```

### セクション F: テストとバリデーション

#### 1. テーマテストスイート

```python
import pytest
from pytest_qt.qtbot import QtBot
from PySide6.QtWidgets import QApplication

class TestThemeSystem:
    """テーマシステムのテストスイート"""

    @pytest.fixture
    def theme_manager(self, qtbot):
        app = QApplication.instance()
        if not app:
            app = QApplication([])
        return ThemeManager(app)

    def test_theme_switching(self, theme_manager, qtbot):
        """テーマ切り替えテスト"""
        # ダークテーマ適用
        theme_manager.apply_theme("dark")
        assert theme_manager.current_theme == "dark"

        # パレット確認
        palette = QApplication.instance().palette()
        window_color = palette.color(QPalette.Window)
        assert window_color.name() == "#232428"

        # ライトテーマ切り替え
        theme_manager.apply_theme("light")
        assert theme_manager.current_theme == "light"

    def test_widget_repaint(self, theme_manager, qtbot):
        """ウィジェット再描画テスト"""
        widget = ThemedWidget()
        qtbot.addWidget(widget)

        with qtbot.waitSignal(theme_manager.theme_changed):
            theme_manager.apply_theme("dark")

        # paintEventが呼ばれたことを確認
        assert widget.palette().color(QPalette.Window).name() == "#232428"

    def test_contrast_ratio(self, theme_manager):
        """コントラスト比テスト"""
        for theme_name in ["dark", "light"]:
            theme_manager.apply_theme(theme_name)
            palette = QApplication.instance().palette()

            ratio = calculate_contrast_ratio(
                palette.color(QPalette.Window),
                palette.color(QPalette.WindowText)
            )

            assert ratio >= 4.5, f"{theme_name}テーマのコントラスト比が不足: {ratio}"
```

#### 2. スタイルバリデーター

```python
class StyleValidator:
    """スタイル定義の検証"""

    @staticmethod
    def validate_theme_json(theme_path: Path) -> List[str]:
        """テーマJSONの検証"""
        errors = []

        with open(theme_path, 'r', encoding='utf-8') as f:
            theme = json.load(f)

        # 必須フィールド確認
        required = ['name', 'version', 'colors', 'dimensions']
        for field in required:
            if field not in theme:
                errors.append(f"必須フィールド '{field}' が不足")

        # 色値の検証
        if 'colors' in theme:
            for key, value in theme['colors'].items():
                if isinstance(value, str) and not value.startswith('#'):
                    errors.append(f"無効な色値: {key}={value}")

        return errors

    @staticmethod
    def validate_qss(qss_content: str) -> List[str]:
        """QSSの検証"""
        errors = []

        # 直接色指定の検出
        import re
        direct_colors = re.findall(r'#[0-9a-fA-F]{6}|rgb\([^)]+\)', qss_content)
        if direct_colors:
            errors.append(f"直接色指定が検出されました: {direct_colors[:3]}...")

        # palette()参照の推奨
        if 'background-color:' in qss_content and 'palette(' not in qss_content:
            errors.append("background-colorにpalette()参照を使用してください")

        return errors
```

### セクション G: マイグレーションガイド

#### 1. 既存コードの移行手順

```python
class ThemeMigrator:
    """既存コードのテーマ対応移行ツール"""

    def __init__(self):
        self.issues = []
        self.fixes = []

    def analyze_file(self, file_path: Path) -> Dict:
        """ファイルの分析"""
        with open(file_path, 'r', encoding='utf-8') as f:
            content = f.read()

        analysis = {
            'file': str(file_path),
            'issues': [],
            'suggestions': []
        }

        # 直接色指定の検出
        import re
        direct_colors = re.findall(
            r'setStyleSheet\([^)]*#[0-9a-fA-F]{6}[^)]*\)',
            content
        )

        if direct_colors:
            analysis['issues'].append({
                'type': 'direct_color',
                'count': len(direct_colors),
                'examples': direct_colors[:3]
            })
            analysis['suggestions'].append(
                "setStyleSheet内の直接色指定をpalette()参照に置換"
            )

        # QPaletteの使用確認
        if 'QPalette' not in content and 'palette()' not in content:
            analysis['issues'].append({
                'type': 'no_palette_usage',
                'severity': 'warning'
            })
            analysis['suggestions'].append(
                "QPaletteベースのテーマシステム導入を検討"
            )

        return analysis

    def generate_migration_report(self, project_dir: Path) -> str:
        """移行レポートの生成"""
        report = ["# テーマ移行分析レポート\n"]

        for py_file in project_dir.rglob("*.py"):
            analysis = self.analyze_file(py_file)
            if analysis['issues']:
                report.append(f"\n## {analysis['file']}")
                report.append(f"- 問題数: {len(analysis['issues'])}")

                for issue in analysis['issues']:
                    report.append(f"  - {issue['type']}: {issue.get('count', 'N/A')}")

                report.append("\n### 推奨対応:")
                for suggestion in analysis['suggestions']:
                    report.append(f"- {suggestion}")

        return '\n'.join(report)
```

#### 2. 段階的移行戦略

```markdown
## フェーズ1: 準備（1週間）
- [ ] 現状分析レポートの生成
- [ ] テーママネージャーの実装
- [ ] 基本テーマ定義（dark/light）の作成
- [ ] テストスイートの準備

## フェーズ2: コア実装（2週間）
- [ ] アプリケーションへのThemeManager統合
- [ ] Fusionスタイルの適用
- [ ] 基本QPalette設定
- [ ] グローバルQSSの適用

## フェーズ3: コンポーネント移行（3週間）
- [ ] 直接色指定の検出と置換
- [ ] カスタムウィジェットのThemedWidget継承
- [ ] WidgetFactoryの導入
- [ ] 各コンポーネントのテスト

## フェーズ4: 検証と最適化（1週間）
- [ ] 全テーマでの動作確認
- [ ] パフォーマンステスト
- [ ] アクセシビリティ検証
- [ ] ドキュメント整備
```

## 信頼性評価

### 高信頼性（スコア 8-10）
- QPaletteベースの設計アプローチ [1][2] - Qt公式ドキュメント準拠
- Fusionスタイル必須性 [4] - Stack Overflow実証済み回答
- pytest-qtテストフレームワーク [7] - 公式PyPIパッケージ

### 中信頼性（スコア 5-7）
- qt-materialライブラリ [3] - 広く使用されているサードパーティ
- デザインパターン実装例 [5] - Medium記事・実践例
- HiDPI対応手法 [9] - コミュニティ実践

### 要検証（スコア ≤4）
- 特定のパフォーマンス最適化手法 - 環境依存の可能性
- 一部のアクセシビリティ実装 - Qt6での動作未検証

## ベストプラクティス要約

### 1. アーキテクチャ設計
- **シングルトンパターン**でThemeManagerを実装
- **ファクトリーパターン**で統一されたウィジェット生成
- **オブザーバーパターン**でテーマ変更を伝播

### 2. 実装ルール
- 必ず`app.setStyle("Fusion")`を使用
- 色は常に`palette()`参照で指定
- テーマ定義はJSON外部化
- カスタムウィジェットは基底クラス継承

### 3. 品質保証
- コントラスト比 4.5:1 以上を維持
- pytest-qtによる自動テスト
- テーマ切り替え時の再描画確認
- HiDPI環境での検証

### 4. 保守性
- デザイントークンによる一元管理
- コンポーネントカタログの維持
- 段階的移行戦略の採用
- 継続的なスタイル検証

## 参考URL

[1] Qt for Python公式ドキュメント - QPalette
https://doc.qt.io/qtforpython-6/PySide6/QtGui/QPalette.html

[2] Styling the Widgets Application - Qt for Python
https://doc.qt.io/qtforpython-6/tutorials/basictutorial/widgetstyling.html

[3] qt-material - Material inspired stylesheet for PySide6
https://pypi.org/project/qt-material/

[4] Stack Overflow - How do I use QT6 Dark Theme with PySide6?
https://stackoverflow.com/questions/73060080/how-do-i-use-qt6-dark-theme-with-pyside6

[5] Medium - Style using PySide6
https://medium.com/@wintersweet001/style-using-pyside6-28c5f8683306

[6] PySide6 PyPI公式ページ
https://pypi.org/project/PySide6/

[7] pytest-qt - pytest plugin for Qt application testing
https://pypi.org/project/pytest-qt/

[8] Qt for Python Development Notes 2024
https://wiki.qt.io/Qt_for_Python_Development_Notes_2024

[9] Python GUIs - PySide6 Tutorial 2025
https://www.pythonguis.com/pyside6-tutorial/

---

```json
{
  "handoff": {
    "recommended_type": "implementation_guide",
    "audience": "developers",
    "key_messages": [
      "QPaletteベースの設計が最重要",
      "統一性維持にはファクトリーパターンが有効",
      "テスト自動化で品質保証",
      "段階的移行で既存コードに対応"
    ],
    "asset_suggestions": [
      "テーマ定義JSONテンプレート",
      "コンポーネントカタログHTML",
      "移行チェックリストExcel",
      "自動テストCI/CD設定"
    ]
  }
}
```