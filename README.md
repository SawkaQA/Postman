# Postman

## HOMEWORK 2 [Collection](https://github.com/SawkaQA/Postman/blob/main/HW_2.postman_collection.json) [Environment](https://github.com/SawkaQA/Postman/blob/main/QA.postman_environment.json)

```javascript
## /first

// 1. Проверить, что в body приходит правильный string.
pm.test("Body is correct", function () {
pm.response.to.have.body("This is the first responce from server!ss");
});

______________
## /user_info_3
______________
// 3. Спарсить response body в json.
let req = request.data;
let req_age = req.age;
let req_name = req.name;
let req_salary = req.salary;
let req_salary_1_5 = req.u_salary_1_5_year;

// 4. Проверить, что name в ответе равно name c request (name вбить руками.)
pm.test("Request and responce name check manual", function () {
    pm.expect(resp_name).to.eql("Sasha");
});

// 5. Проверить, что age в ответе равно age c request (age вбить руками.)
pm.test("Request and responce age check manual", function () {
    pm.expect(+resp_age).to.eql(25);
});

// 6. Проверить, что salary в ответе равно salary c request (salary вбить руками.)
pm.test("Request and responce salary check manual", function () {
    pm.expect(+resp_salary).to.eql(1500);
});

// 7. Спарсить request.
let resp = pm.response.json();
let resp_age = resp.age;
let resp_name = resp.name;
let resp_salary = resp.salary;
let resp_salary_1_5 = resp.u_salary_1_5_year;

// 8. Проверить, что name в ответе равно name c request (name забрать из request.)
pm.test("Request and responce name check", function () {
    pm.expect(resp_name).to.eql(req_name);
});

// 9. Проверить, что age в ответе равно age s request (age забрать из request.)
pm.test("Request and responce age check", function () {
    pm.expect(+resp_age).to.eql(+req_age);
});

// 10. Проверить, что salary в ответе равно salary s request (salary забрать из request.)
pm.test("Request and responce salary check", function () {
    pm.expect(+resp_salary).to.eql(+req_salary);
});

// 11. Вывести в консоль параметр family из response.
console.log("Family ", resp.family);

// 12. Проверить что u_salary_1_5_year в ответе равно salary*4 (salary забрать из request)
pm.test("Check responce salary for 1.5 year and request salary * 4", function () {
    pm.expect(+resp_salary_1_5).to.eql(+req_salary_1_5);
});

pm.test("Status code is 200", function () {
    pm.response.to.have.status(200);
});

______________
## /object_info_3
______________
// 3. Спарсить response body в json.
var resp = pm.response.json();
var resp_name = resp.name;
var resp_age = resp.age;
var resp_salary = resp.salary

// 4. Спарсить request.
var req_url = pm.request.url.query.toObject();
var req_name = req_url.name;
var req_age = req_url.age;
var req_salary = req_url.salary;
var dogname = resp.family.pets.dog;

// 5. Проверить, что name в ответе равно name s request (name забрать из request.)
pm.test("Responce name = request name", function () {
    pm.expect(req_name).to.eql(resp_name);
});

// 6. Проверить, что age в ответе равно age s request (age забрать из request.)
pm.test("Responce age = request age", function () {
    pm.expect(+req_age).to.eql(+resp_age);
});

// 7. Проверить, что salary в ответе равно salary s request (salary забрать из request.)
pm.test("Responce salary = request salary", function () {
    pm.expect(+req_salary).to.eql(+resp_salary);
});

// 8. Вывести в консоль параметр family из response.
console.log("Family", resp.family);

// 9. Проверить, что у параметра dog есть параметры name.
pm.test("Have property name", function() {
  pm.expect(dogname).to.have.property("name");
});

// 10. Проверить, что у параметра dog есть параметры age.
pm.test("Have property age", function() {
  pm.expect(dogname).to.have.property("age");
});

// 11. Проверить, что параметр name имеет значение Luky.
pm.test("Dog name is Luky", function() {
  pm.expect(dogname).to.have.property("name", "Luky");
});

// 12. Проверить, что параметр age имеет значение 4.
pm.test("Dog age is 4", function() {
  pm.expect(dogname).to.have.property("age", 4);
});

______________
## object_info_4
______________
pm.test("Status code is 200", function () {
    pm.response.to.have.status(200);
});

// 3. Спарсить response body в json.
var resp = pm.response.json();
var resp_name = resp.name;
var resp_age = resp.age;
var resp_salary = resp.salary

// 4. Спарсить request.
var req_url = pm.request.url.query.toObject();
var req_name = req_url.name;
var req_age = req_url.age;
var req_salary = req_url.salary

// 5. Проверить, что name в ответе равно name s request (name забрать из request.)
pm.test("Responce name = request name", function () {
    pm.expect(resp_name).to.eql(req_name);
});

// 6. Проверить, что age в ответе равно age из request (age забрать из request.)
pm.test("Responce age = request age", function () {
    pm.expect(+resp_age).to.eql(+req_age);
});

// 7. Вывести в консоль параметр salary из request.
console.log("Request salary", req_salary);

// 8. Вывести в консоль параметр salary из responce.
console.log("Responce salary", resp_salary);

// 9. Вывести в консоль 0-й элемент параметра salary из response.
console.log("Responce salary", resp_salary[0]);

// 10. Вывести в консоль 1-й элемент параметра salary параметр salary из response.
console.log("Responce salary", resp_salary[1]);

// 11. Вывести в консоль 1-й элемент параметра salary параметр salary из response.
console.log("Responce salary", resp_salary[2]);

// 12. Проверить, что 0-й элемент параметра salary равен salary из request (salary забрать из request.)
pm.test("Responce salary = request salary", function () {
    pm.expect(+resp_salary[0]).to.eql(+req_salary);
});

// 13. Проверить, что 1-й элемент параметра salary равен salary*2 из request (salary забрать из request.)
pm.test("Responce salary = request salary", function () {
    pm.expect(+resp_salary[1]).to.eql(+req_salary * 2);
});

// 14. Проверить, что 2-й элемент параметра salary равен salary*3 из request (salary забрать из request.)
pm.test("Responce salary = request salary", function () {
    pm.expect(+resp_salary[2]).to.eql(+req_salary * 3);
});

// 15. Создать в окружении переменную name
pm.environment.get("name");

// 16. Создать в окружении переменную age
pm.environment.get("age");

// 17. Создать в окружении переменную salary
pm.environment.get("salary");

// 18. Передать в окружение переменную name
pm.environment.set("name", req_name);

// 19. Передать в окружение переменную age
pm.environment.set("age", req_age);

// 20. Передать в окружение переменную salary
pm.environment.set("salary", req_salary);

// 21. Написать цикл который выведет в консоль по порядку элементы списка из параметра salary.
for (i in resp_salary) {
    console.log("Key "+ i, "value " + resp_salary[i]);
};

______________
## /user_info_2
______________
// 6. Спарсить response body в json.
let resp = pm.response.json();
let resp_salary_after_1_5_year = resp["qa_salary_after_1.5_year"];
let resp_salary_after_12_months = resp.qa_salary_after_12_months;
let resp_salary_after_3_5_years = resp["qa_salary_after_3.5_years"];
let resp_salary_after_6_months = resp.qa_salary_after_6_months;
let resp_start_qa_salary = resp.start_qa_salary;
// console.log(typeof(respArrName));

// 7. Спарсить request.
let req = request.data;
let req_salary = req.salary;
let req_age = req.age;

// 8. Проверить, что json response имеет параметр start_qa_salary
pm.test("Response have start_qa_salary", function() {
  pm.expect(resp).to.have.property("start_qa_salary");
});

// 9. Проверить, что json response имеет параметр qa_salary_after_6_months
pm.test("Response have qa_salary_after_6_months", function() {
  pm.expect(resp).to.have.property("qa_salary_after_6_months");
});

// 10. Проверить, что json response имеет параметр qa_salary_after_12_months
pm.test("Response have qa_salary_after_12_months", function() {
  pm.expect(resp).to.have.property("qa_salary_after_12_months");
});

// 11. Проверить, что json response имеет параметр qa_salary_after_1.5_year
pm.test("Response have qa_salary_after_1.5_year", function() {
  pm.expect(resp).to.have.property("qa_salary_after_1.5_year");
});

// 12. Проверить, что json response имеет параметр qa_salary_after_3.5_years
pm.test("Response have qa_salary_after_3.5_year", function() {
  pm.expect(resp).to.have.property("qa_salary_after_3.5_years");
});

// 13. Проверить, что json response имеет параметр person
pm.test("Response have person", function() {
  pm.expect(resp).to.have.property("person");
});

// 14. Проверить, что параметр start_qa_salary равен salary из request (salary забрать из request.)
pm.test("Start_qa_salary = request salary", function () {
    pm.expect(resp_start_qa_salary).to.eql(+req.salary);
});

// 15. Проверить, что параметр qa_salary_after_6_months равен salary*2 из request (salary забрать из request.)
pm.test("resp_salary_after_6_months = request salary * 2", function () {
    pm.expect(resp_salary_after_6_months).to.eql(+req.salary * 2);
});

// 16. Проверить, что параметр qa_salary_after_12_months равен salary*2.7 из request (salary забрать из request.)
pm.test("resp_salary_after_12_months = request salary * 2.7", function () {
    pm.expect(resp_salary_after_12_months).to.eql(+req.salary * 2.7);
});

// 17. Проверить, что параметр qa_salary_after_1.5_year равен salary*3.3 из request (salary забрать из request.)
pm.test("resp_salary_after_1.5_year = request salary * 3.3", function () {
    pm.expect(resp_salary_after_1_5_year).to.eql(+req.salary * 3.3);
});

// 18. Проверить, что параметр qa_salary_after_3.5_years равен salary*3.8 из request (salary забрать из request.)
pm.test("resp_salary_after_3.5_years = request salary * 3.8", function () {
    pm.expect(resp_salary_after_3_5_years).to.eql(+req.salary * 3.8);
});

// 19. Проверить, что в параметре person, 1-й элемент из u_name равен salary из request (salary забрать из request.)
pm.test("person.u_name[1]= request salary", function () {
    pm.expect(resp.person.u_name[1]).to.eql(+req.salary);
});

// 20. Проверить, что что параметр u_age равен age из request (age забрать из request.)
pm.test("person.u_age = request age", function () {
    pm.expect(resp.person.u_age).to.eql(+req.age);
});

// 21. Проверить, что параметр u_salary_5_years равен salary*4.2 из request (salary забрать из request.)
pm.test("resp_salary_after_5_years = request salary * 4.2", function () {
    pm.expect(resp.person.u_salary_5_years).to.eql(+req.salary * 4.2);
});

// 22. ***Написать цикл который выведет в консоль по порядку элементы списка из параметра person.
let respArrName = resp.person.u_name;

for (key in resp.person) {
  if (Array.isArray(resp.person[key])) {
    resp.person[key].forEach(val => console.log(val));
} else {
console.log(`${key}: ${resp.person[key]}`);
 }
}
```

## HOMEWORK 3 [Collection]() [Environment]()

```javascript

## /login
// 1) необходимо залогиниться
// Приходящий токен необходимо передать во все остальные запросы.
// ===================
// дальше все запросы требуют наличие токена.
// ===================

let resp = pm.response.json();
let resp_token = resp.token;
pm.environment.set("token", resp_token);

______________
## /user_info
______________
// Тесты:
// 1) Статус код 200
pm.test("Status code is 200", function () {
    pm.response.to.have.status(200);
});

// 2) Проверка структуры json в ответе.
let resp = pm.response.json();

const schema = {
    "type": "object",
    "properties": {
        "start_qa_salary": {"type": "number"},
        "qa_salary_after_6_months": {"type": "number"},
        "qa_salary_after_12_months": {"type": "number"},
        "person":{
            "type": "object",
            "properties": {
                "u_name": {
                    "type": "array",
                    "items": [
                        {"type": "string"},
                        {"type": "integer"},
                        {"type": "integer"}
                    ]
                    },
                "u_age": {"type": "number"},
                "u_salary_1_5_year": {"type": "number"}
            },
            "additionalProperties": false
        }
    },
    "additionalProperties": false
};
pm.test('Schema is valid', function() {
  pm.response.to.have.jsonSchema(schema);
});

// 3) В ответе указаны коэффициенты умножения salary, напишите тесты по проверке правильности результата перемножения на коэффициент.
let resp_qa_sal_x2 = resp.qa_salary_after_6_months;

pm.test("Check salary * 2", function () {
    pm.expect(resp_qa_sal_x2).to.eql(resp.person.u_name[1]*2);
});

let resp_qa_sal_x2_9 = resp.qa_salary_after_12_months;

pm.test("Check salary * 2.9", function () {
    pm.expect(resp_qa_sal_x2_9).to.eql(resp.person.u_name[1]*2.9);
});

let resp_qa_sal_x4 = resp.person.u_salary_1_5_year;

pm.test("Check salary * 4", function () {
    pm.expect(resp_qa_sal_x4).to.eql(resp.person.u_name[1]*4);
});

// 4) Достать значение из поля 'u_salary_1.5_year' и передать в поле salary запроса http://162.55.220.72:5005/get_test_user
pm.environment.set("salary", resp_qa_sal_x4);


______________
## /new_data
______________
// Тесты:
// 1) Статус код 200
pm.test("Status code is 200", function () {
    pm.response.to.have.status(200);
});

// 2) Проверка структуры json в ответе.
let resp = pm.response.json();

const schema = {
    "type": "object",
    "properties": {
    "age": {
      "type": "integer"
    },
    "name": {
      "type": "string"
    },
    "salary": {
      "type": "array",
      "items": [
        {
          "type": "integer"
        },
        {
          "type": "string"
        },
        {
          "type": "string"
        }  
      ]
    }
  },
  "additionalProperties": false
}
pm.test('Schema is valid', function() {
  pm.response.to.have.jsonSchema(schema);
});

// 3) В ответе указаны коэффициенты умножения salary, напишите тесты по проверке правильности результата перемножения на коэффициент.
let resp_sal = resp.salary[0];
let resp_sal_x2 = +resp.salary[1];
let resp_sal_x3 = +resp.salary[2];

pm.test("Check salary * 2", function () {
    pm.expect(resp_sal_x2).to.eql(resp.salary[0]*2);
});

pm.test("Check salary * 3", function () {
    pm.expect(resp_sal_x3).to.eql(resp.salary[0]*3);
});

// 4) проверить, что 2-й элемент массива salary больше 1-го и 0-го
pm.test("salary[2] > salary[0] and salary[2] > salary[1]", function(){
    pm.expect(+resp.salary[2]).to.greaterThan(resp.salary[0])
    pm.expect(+resp.salary[2]).to.greaterThan(+resp.salary[1])
})
// function CheckSalary() {
//     if ((resp_sal_x3 > resp_sal_x2) && (resp_sal_x3 > resp_sal)) {
//         console.log(true)
// } else {
//         console.log(false) 
//     }
// }
// CheckSalary();

______________
## /test_pet_info
______________
// Тесты:
// 1) Статус код 200
pm.test("Status code is 200", function () {
    pm.response.to.have.status(200);
});

// 2) Проверка структуры json в ответе.
let resp = pm.response.json();

const schema = {
  "type": "object",
  "properties": {
    "age": {
      "type": "integer"
    },
    "daily_food": {
      "type": "number"
    },
    "daily_sleep": {
      "type": "number"
    },
    "name": {
      "type": "string"
    }
  },
  "required": [
    "age",
    "daily_food",
    "daily_sleep",
    "name"
  ]
}
pm.test('Schema is valid', function() {
  pm.response.to.have.jsonSchema(schema);
});

// 3) В ответе указаны коэффициенты умножения weight, напишите тесты по проверке правильности результата перемножения на коэффициент.
let resp_daily_food = resp.daily_food;
let resp_daily_sleep = resp.daily_sleep;

let req = request.data
let req_weight = +req.weight;


pm.test("Check weight for daily food", function () {
    pm.expect(resp_daily_food).to.eql(req_weight * 0.012);
});

pm.test("Check weight for daily sleep", function () {
    pm.expect(resp_daily_sleep).to.eql(req_weight * 2.5);
});

______________
## /get_test_user
______________
// Тесты:
// 1) Статус код 200
pm.test("Status code is 200", function () {
    pm.response.to.have.status(200);
});

// 2) Проверка структуры json в ответе.
let resp = pm.response.json();

const schema = {
  "type": "object",
  "properties": {
    "age": {
      "type": "string"
    },
    "family": {
      "type": "object",
      "properties": {
        "children": {
          "type": "array",
          "items": [
            {
              "type": "array",
              "items": [
                {
                  "type": "string"
                },
                {
                  "type": "integer"
                }
              ]
            },
            {
              "type": "array",
              "items": [
                {
                  "type": "string"
                },
                {
                  "type": "integer"
                }
              ]
            }
          ]
        },
        "u_salary_1_5_year": {
          "type": "integer"
        }
      },
      "required": [
        "children",
        "u_salary_1_5_year"
      ]
    },
    "name": {
      "type": "string"
    },
    "salary": {
      "type": "integer"
    }
  },
  "required": [
    "age",
    "family",
    "name",
    "salary"
  ]
}
pm.test('Schema is valid', function() {
  pm.response.to.have.jsonSchema(schema);
});

// 3) Проверить что занчение поля name = значению переменной name из окружения
let resp_name = resp.name;
let resp_age = resp.age;

pm.test("Name = Env name", function () {
    pm.expect(pm.environment.get("name")).to.equal(resp_name);
});

// 4) Проверить что занчение поля age в ответе соответсвует отправленному в запросе значению поля age
let req = request.data
let req_age = req.age;

pm.test("Resp age = req age", function () {
    pm.expect(req_age).to.eql(resp_age);
});

______________
## /currency
______________
// Тесты:
// 1) Можете взять любой объект из присланного списка, используйте js random.
let resp = pm.response.ison();
let randomObj =resp[Math.floor(Math.random() * resp.length)];
pm.environment.set ("Cur_ID", randomObj.Cur_ID)

// В объекте возьмите Cur_ID и передать через окружение в следующий запрос.
let curId = pm.environment.get("Cur_ID")

______________
## /curr_byn
______________
// Тесты:
// 1) Статус код 200
pm.test("Status code is 200", function () {
    pm.response.to.have.status(200);
});

// 2) Проверка структуры json в ответе.
const schema = {
    "type": "object",
    "properties": {
    "Cur_Abbreviation": {"type": "string"},
    "Cur_ID": {"type": "integer"},
    "Cur_Name": {"type": "string"},
    "Cur_OfficialRate": {"type": "number"},
    "Cur_Scale": {"type": "integer"},
    "Date": {"type": "string"}
    },
    "additionalProperties": false
}
pm.test("json is valid", function(){
    pm.response.to.have.jsonSchema(schema);
})

// 1) получить список валют
// 2) итерировать список валют
// 3) в каждой итерации отправлять запрос на сервер для получения курса каждой валюты
// 4) если возвращается 500 код, переходим к следующей итреации
// 5) если получаем 200 код, проверяем response json на наличие поля "Cur_OfficialRate"
// 6) если поле есть, пишем в консоль инфу про фалюту в виде response
// 7) переходим к следующей итерации

let resp = pm.response.json()
let arrLenght = resp.length

let randomObj =resp[Math.floor(Math.random() * resp.length)];
pm.environment.set ("Cur_ID", randomObj.Cur_ID)

let curId = 0;
let token = pm.environment.get("token")  

for(let i = 0; i < arrLenght; i++){
    curId = resp[i].Cur_ID;
    const regRequest = {
        'method': 'POST',
        'url': 'http://162.55.220.72:5005/curr_byn',
        'body': {
            'mode': 'formdata',
            'formdata': [
                {'key': 'auth_token', 'value': token},
                {'key': 'curr_code', 'value': curId}
            ]
        }
    };
    pm.sendRequest(regRequest, (err, res) => {
        if(res.code == 200){
            let resp = response.json();
            if(pm.expect(resp).have.to.property("Cur_OfficialRate")){
                console.log(resp)
            };
        }
    });
}
```
