# Домашнее задание к занятию «Безопасность в облачных провайдерах» - Вдовин Вадим

Используя конфигурации, выполненные в рамках предыдущих домашних заданий, нужно добавить возможность шифрования бакета.

---
## Задание 1. Yandex Cloud   

> 1. С помощью ключа в KMS необходимо зашифровать содержимое бакета:
> 
>  - создать ключ в KMS;
>  - с помощью ключа зашифровать содержимое бакета, созданного ранее.
>
> 2. (Выполняется не в Terraform)* Создать статический сайт в Object Storage c собственным публичным адресом и сделать доступным по HTTPS:
> 
>  - создать сертификат;
>  - создать статическую страницу в Object Storage и применить сертификат HTTPS;
>  - в качестве результата предоставить скриншот на страницу с сертификатом в заголовке (замочек).
> 
> Полезные документы:
> 
> - [Настройка HTTPS статичного сайта](https://cloud.yandex.ru/docs/storage/operations/hosting/certificate).
> - [Object Storage bucket](https://registry.terraform.io/providers/yandex-cloud/yandex/latest/docs/resources/storage_bucket).
> - [KMS key](https://registry.terraform.io/providers/yandex-cloud/yandex/latest/docs/resources/kms_symmetric_key).


### Решение:
С помощью Terraform развернул все необходимые ресурсы в Yandex Cloud

Выполнил `terraform apply`:
![01](https://github.com/user-attachments/assets/d68ad972-8867-4280-be46-8e507f406a8b)

1. Дополнил бакет из прошлого задания, создал ключ KMS и зашифровал содержимое.
    ![02](https://github.com/user-attachments/assets/69c3ef03-7b10-419e-8fb6-7f5d65baea9c)
    ![03](https://github.com/user-attachments/assets/bc5f305f-c9b8-4deb-8f72-372dab7ec304)
    Файл извне недоступен для прочтения:
   ![04](https://github.com/user-attachments/assets/86b4a7c6-5d14-4aee-ad86-3d7e8a993e6b)

---
2. Для выполнения 2 задания зарегистрировал домен, настроил у регистратора записи NS, выпустил в YC сертификат и подтвердил владение доменом:
    ![06](https://github.com/user-attachments/assets/e642af26-d1b0-412a-8e14-7228097aa929)
    С помощью Terraform создал отдельный бакет для хостинга статического сайта, а также настроил https и хостинг автоматически.
    Проверил доступность и сертификат на сайте:
    ![05](https://github.com/user-attachments/assets/a87145aa-edb6-4142-a522-7e57e9ce8635)
