# Image_scrap
🤖Image Scraping is fun with Selenium lib in Python, Image mining can be so easy and automated. if we can utilize the foundation of programming. Basically, I am using a bunch of simple code to gather data through a google search engine. At the same time, it also allows me to download all similar images from google images.
I am using Jupyter Notebook, and python libs such as selenium, requests, pillow, time, and image. I am using google chrome, so chrome driver is essential for my search. 
[![Linkedin](https://img.shields.io/website?label=Linkedin&style=for-the-badge&url=https://www.linkedin.com/in/thapahemant/)](https://www.linkedin.com/in/thapahemant/)


# Selenium

<img width="1000" align='center' src="https://raw.githubusercontent.com/harryworlds/harryworlds/main/mech_can_code.png">

<img width="1000" align='center' src="https://github.com/harryworlds/image_scrap/blob/main/gif.gif">

<img width="1000" align='center' src="https://raw.githubusercontent.com/harryworlds/image_scrap/main/code.png">



---

<br/>
# <> CODE IS HERE <>

<!--START_SECTION:waka-->

```text
from selenium import webdriver
from selenium.webdriver.common.by import By
import requests
import io
from PIL import Image
import time


PATH = "C:\\Users\\heman\\Desktop\\Web_scrap\\chromedriver.exe"

wd = webdriver.Chrome(PATH)

def get_images_from_google(wd, delay, max_images):
	def scroll_down(wd):
		wd.execute_script("window.scrollTo(0, document.body.scrollHeight);")
		time.sleep(delay)

	url = input()
	wd.get(url)

	image_urls = set()
	skips = 0

	while len(image_urls) + skips < max_images:
		scroll_down(wd)

		thumbnails = wd.find_elements(By.CLASS_NAME, "Q4LuWd")

		for img in thumbnails[len(image_urls) + skips:max_images]:
			try:
				img.click()
				time.sleep(delay)
			except:
				continue

			images = wd.find_elements(By.CLASS_NAME, "n3VNCb")
			for image in images:
				if image.get_attribute('src') in image_urls:
					max_images += 1
					skips += 1
					break

				if image.get_attribute('src') and 'http' in image.get_attribute('src'):
					image_urls.add(image.get_attribute('src'))
					print(f"Image {len(image_urls)}")

	return image_urls


def download_image(download_path, url, file_name):
	try:
		image_content = requests.get(url).content
		image_file = io.BytesIO(image_content)
		image = Image.open(image_file)
		file_path = download_path + file_name

		with open(file_path, "wb") as f:
			image.save(f, "JPEG")

		print("Success downloaded")
	except Exception as e:
		print('Error -', e)
initial_value = 1
final_value = 10
urls = get_images_from_google(wd, initial_value, final_value)

for harryworlds, url in enumerate(urls):
	download_image("download_images/", url, str(harryworlds) + ".jpg")
print(wd)


```

<!--END_SECTION:waka-->

---

Thansk for reading and hopefully, you enjyoed it.
<br/>
---
[![Linkedin](https://img.shields.io/website?label=Linkedin&style=for-the-badge&url=https://www.linkedin.com/in/thapahemant/)](https://www.linkedin.com/in/thapahemant/)

[![Website](https://img.shields.io/website?label=Click_here/harryworls_Github&style=for-the-badge&url=https://github.com/harryworlds)](https://github.com/harryworlds)
