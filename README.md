# Adonis Enum

## How To Use
Installation
```bash
npm i adonis-enum --save
```

Stored inside the app/Enums/... directory
```javascript
const Enum = require('adonis-enum')

module.exports = new Enum({
  SUPERADMIN: 1,
  CUSTOMER: 2
})
```
### Example
use in validation
```javascript
const RoleEnum = use('App/Enums/RoleEnum')

console.log(RoleEnum.valuesString) // 1,2
console.log(RoleEnum.valuesStringWithSpace) // 1, 2
console.log(RoleEnum.keysString) // SUPERADMIN,CUSTOMER
console.log(RoleEnum.keysStringWithSpace) // SUPERADMIN, CUSTOMER

get rules () {
  return {
    role: `required|in:${RoleEnum.valuesString}`
  }
}

get messages () {
  return {
    'role.in': `The role field does not exist in ${RoleEnum.valuesStringWithSpace}`.
  }
}
```

use in Factory
```javascript
const Factory = use('Factory')
const RoleEnum = use('App/Enums/RoleEnum')

console.log(RoleEnum.values) // [1, 2]
console.log(RoleEnum.keys) // ['SUPERADMIN', 'CUSTOMER']

Factory.blueprint('App/Models/User', (faker) => {
  return {
    role: faker.pickone(RoleEnum.values),
  }
})
```

use in Model
```javascript
const RoleEnum = use('App/Enums/RoleEnum')

console.log(RoleEnum.make(1).key) // 'SUPERADMIN'
console.log(RoleEnum.make(2).key) // 'CUSTOMER'

console.log(RoleEnum.make(1).value) // 1
console.log(RoleEnum.make(2).value) // 2

console.log(RoleEnum.has('BACKOFFICE')) // false
console.log(RoleEnum.has('SUPERADMIN')) // true

console.log(RoleEnum.SUPERADMIN.value === 2) // false
console.log(RoleEnum.SUPERADMIN.value === 1) // true

class User extends Model {
  getRole (role) {
    return RoleEnum.make(role).key
  }
}
```


## License
Copyright (c) 2021

Permission is hereby granted, free of charge, to any person obtaining a copy of this software and associated documentation files (the "Software"), to deal in the Software without restriction, including without limitation the rights to use, copy, modify, merge, publish, distribute, sublicense, and/or sell copies of the Software, and to permit persons to whom the Software is furnished to do so, subject to the following conditions:

The above copyright notice and this permission notice shall be included in all copies or substantial portions of the Software.

THE SOFTWARE IS PROVIDED "AS IS", WITHOUT WARRANTY OF ANY KIND, EXPRESS OR IMPLIED, INCLUDING BUT NOT LIMITED TO THE WARRANTIES OF MERCHANTABILITY, FITNESS FOR A PARTICULAR PURPOSE AND NONINFRINGEMENT. IN NO EVENT SHALL THE AUTHORS OR COPYRIGHT HOLDERS BE LIABLE FOR ANY CLAIM, DAMAGES OR OTHER LIABILITY, WHETHER IN AN ACTION OF CONTRACT, TORT OR OTHERWISE, ARISING FROM, OUT OF OR IN CONNECTION WITH THE SOFTWARE OR THE USE OR OTHER DEALINGS IN THE SOFTWARE.
