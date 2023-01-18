# praktikum-11

## penjelasan

!pip install pandas digunakan untuk menginstall package pandas di python. Package pandas digunakan untuk memanipulasi data dalam bentuk tabel (dataframe) dan digunakan untuk data analysis. Fungsi dari package pandas sangat luas, seperti melakukan operasi pada data, mengimport dan mengeksport data dari berbagai format, dan lainnya. !pip install requests digunakan untuk menginstall package requests di python. Package requests digunakan untuk melakukan HTTP request dari python.

!pip install BeautifulSoup4 digunakan untuk menginstall package BeautifulSoup4 di python. Package BeautifulSoup4 digunakan untuk parsing dan mengelola data dari HTML atau XML.

import pandas as pd digunakan untuk mengimport library pandas dan menyebutnya sebagai pd. Library pandas digunakan untuk memanipulasi data dalam bentuk tabel (dataframe) dan digunakan untuk data analysis.

from bs4 import BeautifulSoup digunakan untuk mengimport class BeautifulSoup dari package BeautifulSoup4. Class BeautifulSoup digunakan untuk mengelola dan mengolah data dari HTML atau XML.

## gunakan import supaya bisa tersambung dengan pip-nya

  Source code : 

    import requests
    from bs4 import BeautifulSoup
    import pandas as pd

## lalu masukkan code untuk membuat nya

  Source code :

    URL = "https://glints.com/id/lowongan-kerja"
    req = requests.get(URL)
    soup = BeautifulSoup(req.content, 'html.parser')
    jobs = soup.find_all('div', attrs={'id':'__next'})
    job_titles = []
    job_locations = []
    companies = []
    for job in jobs:
        job_title = job.find('h2', attrs={'class': 'CompactOpportunityCardsc__JobTitle-sc-1y4v110-8 cYZbCX'})
        job_titles.append(job_title)
        location = job.find('div', attrs={'class': 'CompactOpportunityCardsc__OpportunityInfo-sc-1y4v110-12 ikxvyY'})
        job_locations.append(location)
        company = job.find('div', attrs={'class':'CompactOpportunityCardsc__Ellipsis-sc-1y4v110-9 bsrUTu'})
        companies.append(company)
    datanya = pd.DataFrame({'Pekerjaan': job_titles, 'Lokasi': locations, 'Perusahaan': companies})
    print(datanya)

## penjelasan

mengambil data lowongan kerja dari situs web Glints. Dengan menggunakan library Python 'requests', kodingan mengirim permintaan GET ke URL "https://glints.com/id/lowongan-kerja" yang merupakan halaman web yang berisi informasi lowongan kerja. Kemudian, dengan menggunakan library 'BeautifulSoup', kodingan menganalisis konten halaman web yang didapat dari permintaan GET tersebut dengan menggunakan parser HTML.

Selanjutnya, kodingan mencari semua elemen HTML dengan atribut 'div' dan 'id' yang sesuai, yaitu '__next'. Kemudian, dari elemen-elemen tersebut, kodingan mengekstrak informasi pekerjaan, lokasi, dan nama perusahaan dengan mencari elemen yang memiliki atribut 'class' yang sesuai. Informasi yang diambil kemudian disimpan dalam sebuah list yang sesuai.

Setelah itu, kodingan menggunakan library pandas untuk membuat dataframe dari list yang didapat dan menyimpannya dalam variabel 'df'. Kemudian kodingan mencetak dataframe tersebut, sehingga kita dapat melihat informasi lowongan kerja yang diambil dari situs web Glints.
