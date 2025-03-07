# Управление оценками в электронном дневнике

Скрипт предназначен для управления оценками и похвалами учеников в системе электронного дневника на основе Django. Он позволяет автоматически исправлять низкие оценки, удалять наказания и создавать похвалы для учеников.

## Использование

### 1. Исправить оценки

Школьник хочет исправить свои оценки, что ему нужно сделать:

1. **Клонировать репозиторий**:
   - Перейдите по [ссылке](https://github.com/Examen33/Haking_Diary.git) на репозиторий GitHub.
   - Клонирует репозиторий на свой сервер.

2. **Скопировать скрипт**:
   - Скопируйте файл со скриптом (например, `skript.py`) в директорию, где находится файл `manage.py` вашего проекта Django.

3. **Установить зависимости**:
   - Убедитесь, что у него установлен Python и Django.
   - Установите необходимые библиотеки из клонированного репозитория п.1:
     ```
     pip install -r requirements.txt
     ```

4. **Настроить переменные окружения**:
   - Создайте файл `.env` в корневой директории проекта и добавьте в него следующие переменные:
     ```
     NAME=<ФИО ученика>
     LESSON=<Название предмета>
     ```

5. **Запустить скрипт**:
   - Откройте консоль и запустите Django shell с помощью команды:
     ```
     python manage.py shell
     ```
   - Импортируйте функции из вашего скрипта и выполните их:
     ```
     from fix_grades import fix_marks, remove_chastisements, create_commendation
     
     # Получите ученика по имени
     from datacenter.models import Schoolkid
     student = Schoolkid.objects.get(full_name=os.getenv('NAME'))
     
     # Исправьте оценки, удалите жалобы и создайте похвалу
     fix_marks(student)
     remove_chastisements(student)
     create_commendation(student, os.getenv('LESSON'))
     ```

6. **Проверить результаты**:
   - Откройте сайт электронного дневника и проверьте, оценки, жалобы и похвалу от учителя.

### 2. Ошибки ввода

Если будет ошибка при вводе данных, скрипт сообщит об этом понятным языком:

- Если он введет неправильное имя или пустую строку, скрипт выведет сообщение об ошибке и объяснит, как это исправить.
- Если он ошибется в названии урока, например, введет "матиматика", скрипт также сообщит об ошибке.
