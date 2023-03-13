# HOMEWORK 2 [Collection](https://github.com/SawkaQA/Postman/blob/main/HW_2.postman_collection.json) [Environment](https://github.com/SawkaQA/Postman/blob/main/QA.postman_environment.json)

```javascript

##/first
// 1. Проверить, что в body приходит правильный string.
pm.test("Body is correct", function () {
pm.response.to.have.body("This is the first responce from server!ss");
});

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
```

# HOMEWORK 3 [Collection]() [Environment]()

```javascript
// 1) необходимо залогиниться
// POST
// http://162.55.220.72:5005/login
// login : str (кроме /)
// password : str

// Приходящий токен необходимо передать во все остальные запросы.

// ===================
// дальше все запросы требуют наличие токена.
// ===================

let resp = pm.response.json();
let resp_token = resp.token;
pm.environment.set("token", resp_token);

// Тесты:
// 1) Статус код 200
pm.test("Status code is 200", function () {
    pm.response.to.have.status(200);
});

// 2) Проверка структуры json в ответе.
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
let resp = pm.response.json();
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
