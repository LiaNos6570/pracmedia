# pracmedia

Задание 3: https://www.figma.com/design/mgVhHBqfjAyVooLEF8QvDT/Untitled?node-id=0-1&p=f&t=FyuMT79eEtC8qHrh-0



Задание 5:
1. Вывести покупателей с количеством осуществленных покупок
SELECT
    Покупатели.Имя,
    Покупатели.Фамилия,
    COUNT(Покупки.Идентификатор) AS Количество_покупок
FROM
    Покупатели
LEFT JOIN
    Покупки ON Покупатели.Идентификатор = Покупки.Ключ_покупателя
GROUP BY
    Покупатели.Идентификатор, Покупатели.Имя, Покупатели.Фамилия;
2. Вывести общую стоимость товаров для каждого покупателя и отсортировать результат в порядке убывания
SELECT
    Покупатели.Имя,
    Покупатели.Фамилия,
    SUM(Товары.Стоимость) AS Общая_стоимость
FROM
    Покупатели
JOIN
    Покупки ON Покупатели.Идентификатор = Покупки.Ключ_покупателя
JOIN
    Товары ON Покупки.Ключ_товара = Товары.Идентификатор
GROUP BY
    Покупатели.Идентификатор, Покупатели.Имя, Покупатели.Фамилия
ORDER BY
    Общая_стоимость DESC;
3. Получить покупателей, купивших только один товар
SELECT
    Покупатели.Имя,
    Покупатели.Фамилия
FROM
    Покупатели
JOIN
    Покупки ON Покупатели.Идентификатор = Покупки.Ключ_покупателя
GROUP BY
    Покупатели.Идентификатор, Покупатели.Имя, Покупатели.Фамилия
HAVING
    COUNT(Покупки.Идентификатор) = 1;
