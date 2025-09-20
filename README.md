# conftest.py
import pytest, os
from selenium import webdriver
from selenium.webdriver.chrome.options import Options
from selenium.webdriver.support.ui import WebDriverWait

@pytest.fixture(scope="session")
def base_url():
    return os.getenv("BASE_URL", "https://example.com")

@pytest.fixture
def driver():
    opts = Options()
    opts.add_argument("--headless=new")
    drv = webdriver.Chrome(options=opts)
    drv.set_window_size(1400, 900)
    yield drv
    drv.quit()

@pytest.fixture
def wait(driver):
    return WebDriverWait(driver, 10)

