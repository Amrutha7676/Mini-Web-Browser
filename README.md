# Mini-Web-Browser
from PyQt5.QtWidgets import QApplication, QMainWindow, QVBoxLayout, QWidget, QLineEdit
from PyQt5.QtWebEngineWidgets import QWebEngineView
from PyQt5.QtCore import QUrl  # <-- Add this import

class Browser(QMainWindow):
    def __init__(self):
        super().__init__()
        self.setWindowTitle("Mini Web Browser")
        self.setGeometry(100, 100, 1000, 600)

        self.browser = QWebEngineView()
        self.browser.setUrl(QUrl("https://www.google.com"))  # <-- Wrap with QUrl

        self.url_bar = QLineEdit()
        self.url_bar.returnPressed.connect(self.load_url)

        layout = QVBoxLayout()
        layout.addWidget(self.url_bar)
        layout.addWidget(self.browser)

        container = QWidget()
        container.setLayout(layout)

        self.setCentralWidget(container)

    def load_url(self):
        url = self.url_bar.text()
        if not url.startswith("http"):
            url = "http://" + url
        self.browser.setUrl(QUrl(url))  # <-- Wrap with QUrl

if __name__ == "__main__":
    import sys
    app = QApplication(sys.argv)
    window = Browser()
    window.show()
    sys.exit(app.exec_())
