# HOMEWORK 2 [Collection](https://github.com/SawkaQA/Postman/blob/main/HW_2.postman_collection.json) [Environment](https://github.com/SawkaQA/Postman/blob/main/QA.postman_environment.json)

1. Проверить, что в body приходит правильный string.
```javascript
    pm.test("Body is correct", function () {
    pm.response.to.have.body("This is the first responce from server!ss");
});
```
