# automation-tests.py
from selenium import webdriver
from selenium.webdriver.common.by import By
import time

# Инициализация драйвера
driver = webdriver.Chrome()
driver.get("https://www.amazon.com")

# Тест: поиск товара и добавление в корзину
try:
    # Поиск товара
    search_box = driver.find_element(By.ID, "twotabsearchtextbox")
    search_box.send_keys("laptop")
    search_box.submit()
    time.sleep(2)

    # Открываем страницу первого товара
    product = driver.find_elements(By.CSS_SELECTOR, ".s-title")[0]
    product.click()
    time.sleep(2)

    # Добавляем товар в корзину
    add_to_cart_btn = driver.find_element(By.ID, "add-to-cart-button")
    add_to_cart_btn.click()
    time.sleep(2)

    # Проверка добавления
    cart_count = driver.find_element(By.ID, "nav-cart-count").text
    assert cart_count == "1", "Ошибка: Товар не добавлен в корзину."

    print("Тест успешно завершен: Товар добавлен в корзину.")
except Exception as e:
    print("Ошибка в тесте:", e)
finally:
    driver.quit()
