# База данных: Вакансии HeadHunter.ru

## Описание
Программа для получения информации о вакансиях с платформы hh.ru в России, сохранения ее в базу данных и отображения необходимых запросов .

## Содержание
1. модули main.py, database.ini и config.py в корне проекта
2. папка data
3. директория src с рабочими модулями
   
#### В модуле main.py описана функция взаимодействия с пользователем

#### Модуль config.py содержит функцию config() для чтения конфигурационных файлов

### Модули директории src:

#### db_creator.py. 
Модуль содержит функцию create_db(db_name, params) для создания базы данных с необходимыми таблицами
params - параметры подключения к базе данных, считываемые из файла database.ini. 

#### Содержание файла:

[postgresql]

   host=localhost
   
   user=postgres
   
   password=ваш_пароль_от_postgresql
   
   port=5432

#### db_manager.py.
В модуле описан класс DBManager для получения информации о вакансиях из базы данных

##### В классе присутствуют 5 методов:

get_companies_and_vacancies_count() (возвращает список работодателей и количество вакансий)

get_all_vacancies() (возвращает список всех вакансий)

get_avg_salary() (возвращает среднюю зарплату по вакансиям)

get_vacancies_with_higher_salary() (возвращает список вакансий, у которых зарплата выше средней)

get_vacancies_with_keyword(keyword) (возвращает список вакансий по ключевому слову в названии)

hh_api.py. Модуль содержит абстрактный класс Parser и класс-наследник HeadHunterAPI

#### class HeadHunterAPI(Parser):
    """Класс для работы с API HeadHunter"""

def __init__(self) -> None:

        """Инициализатор класса HeadHunterAPI"""
        
        self.__url: str = "https://api.hh.ru/vacancies"
        
        self.__headers: dict[str, str] = {"User-Agent": "HH-User-Agent"}
        
        self.__params: dict[str, int] = {"employer_id": "", "page": 0, "per_page": 100}
        
        self.__vacancies: list[dict] = []
        
#### fill_tables.py. 
Модуль содержит функцию enter_data_into_tables() для заполнения базы данных полученной информацией о работодателях и вакансиях

#### utils.py. 
В модуле содержаться функции get_employer_info() и get_vacancy_info(), возвращающие словари с необходимой информацией из ответа, полученного по API
