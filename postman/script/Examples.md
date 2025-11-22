
```json
{
    "message": "من فضلك انتظر الموافقة من الادارة.",
    "data": {
        "user": {
            "id": 218,
            "user_type": "employee",
            "name": "AM",
            "email": null,
            "identity_number": "1000000024",
            "phone": "966500000024",
            "is_active": true,
            "is_accepted": false,
            "company_id": "1",
            "attendance_time": "10:00",
            "leave_time": "15:00",
            "code": null,
            "qr_code": null,
            "notes": "this is notes",
            "plates_count": 1,
            "company": "شركة المجد",
            "plates": [
                {
                    "id": 567,
                    "plate_num": "ب ج د | 15",
                    "station_num": "station_15"
                }
            ]
        }
    }
}
```

```js
pm.test("Response time below 200", function () {
    pm.expect(pm.response.responseTime).to.be.below(200);
});

pm.test("Status code is 202", function () {
    pm.response.to.have.status(202);
});

let response = pm.response.json();

pm.test("Data object exists", function(){
    pm.expect(response).to.have.property("data");
});

pm.test("Data object have user object", function () {
    pm.expect(response.data).to.have.property('user');
});

let user = response.data.user;
if (user.user_type == "employee"){
    pm.test(
        "Employee have (id, user_type, name, email, ...)", 
        function () {
            pm.expect(user).to.have.property('id');
            pm.expect(user).to.have.property('user_type');
            pm.expect(user).to.have.property('name');
            pm.expect(user).to.have.property('email');
            pm.expect(user).to.have.property('identity_number');
            pm.expect(user).to.have.property('phone');
            pm.expect(user).to.have.property('is_active');
            pm.expect(user).to.have.property('is_accepted');
            pm.expect(user).to.have.property('company_id');
            pm.expect(user).to.have.property('attendance_time');
            pm.expect(user).to.have.property('leave_time');
            pm.expect(user).to.have.property('code');
            pm.expect(user).to.have.property('qr_code');
            pm.expect(user).to.have.property('notes');
            pm.expect(user).to.have.property('plates_count');
            pm.expect(user).to.have.property('company');
            pm.expect(user).to.have.property('plates');
        }
    );
    let plates = user.plates
    pm.test(
        "Plates have (id, plate_num, station_num)",
        function(){
            pm.expect(plates).to.be.an('array');
                plates.forEach(function(plate){
                pm.expect(plate).to.have.property('id');
                pm.expect(plate).to.have.property('plate_num');
                pm.expect(plate).to.have.property('station_num');
            });
        } 
    )
} else if (user.user_type == "gaurd"){

}
```