# HOMEWORK 2 [Collection](https://github.com/SawkaQA/Postman/blob/main/HW_2.postman_collection.json) [Environment](https://github.com/SawkaQA/Postman/blob/main/QA.postman_environment.json)

```javascript
// 1. Проверить, что в body приходит правильный string.
pm.test("Body is correct", function () {
pm.response.to.have.body("This is the first responce from server!ss");
});

// 3. Спарсить response body в json.
let resp = pm.response.json();
let resp_age = resp.age;
let resp_name = resp.name;
let resp_salary = resp.salary;
let resp_salary_1_5 = resp.u_salary_1_5_year;

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
let req = request.data;
let req_age = req.age;
let req_name = req.name;
let req_salary = req.salary;
let req_salary_1_5 = req.u_salary_1_5_year;

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
