
from appium import webdriver
from appium.options.android import UiAutomator2Options
from appium.webdriver.common.appiumby import AppiumBy
import time

options = UiAutomator2Options()
options.platform_name = "Android"
options.device_name = "Android"
options.app_package = "com.seuapp"
options.app_activity = ".MainActivity"
options.no_reset = True

driver = webdriver.Remote(
    "http://127.0.0.1:4723",
    options=options
)

try:
    # Abre o menu
    driver.find_element(
        AppiumBy.ACCESSIBILITY_ID,
        "Menu"
    ).click()

    # Clica no botão de anúncio
    driver.find_element(
        AppiumBy.ID,
        "com.seuapp:id/watchAdButton"
    ).click()

    # Aguarda o carregamento
    time.sleep(5)

    # Verifica se o estado esperado apareceu
    reward = driver.find_element(
        AppiumBy.ID,
        "com.seuapp:id/rewardStatus"
    )

    assert reward.text == "Recompensa recebida"

finally:
    driver.quit()
