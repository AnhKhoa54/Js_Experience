# Tham trị và Tham chiếu
Js về bản chất sẽ có 2 kiểu dữ liệu chính:
- Tham trị 
- Tham chiếu

## Kiểu tham trị (Primitive Types)
Sẽ bao gồm các kiểu dữ liệu:
- String
- Number
- Boolean
- Null
- Undefined
- BigInt (Cái này lần đầu biết, hình như trong ES6 mới hỗ trợ)
- Symbol (Cái này cũng lần đầu biết)

#### Việc copy với biến tham trị
- Nó sẽ lấy giạ của biến này và gán vào **một biến độc lập khác**
- Khi thay đổi giá trị của 1 biến nó sẽ không thay đổi giá trị của biến còn lại

## Kiểu tham chiếu (Reference types)
Sẽ bao gồm các kiểu dữ liệu (Thực ra những thằng này đều là object thôi):
- Object
- Array
- Function

#### Việc copy biến với tham chiếu
    let user = { name: 'Anh Khoa' }
    let anotherUser = user // Copy Reference

- Ở đây, user chính là một **biến Object**
- **Một biến Object không lưu trữ giá trị, nó sẽ lưu trữ "địa chỉ ô nhớ" - tham chiếu đến ô nhớ**
- Ở đây, hiểu đơn giản là object { name: 'Anh Khoa' } sẽ được lưu trữ đâu đó ở trong ô nhớ. Biến User sẽ tham chiếu đến ô nhớ đó.
- Khi chúng ta copy một object, thì tức là tham chiếu của nó bị copy, object không bị nhân đôi lên (2 biến cùng tham chiếu vào 1 ô nhớ)


#### So sánh với tham chiếu
    let a = {}
    let b = a // copy Reference

    console.log(a == b) // True (Do 2 thằng cùng tham chiếu đến 1 Object)

    let c = {}
    let d = {}
    console.log(c == d) // False (Do 2 thằng là 2 Object độc lập -- 2 vùng nhớ khác nhau)

## Clone Và Merge
- Như đã biết, khi chúng ta copy 1 Object thì nó sẽ tạo thêm 1 biến khác tham chiếu đến cùng 1 Object
- Trong nhiều trường hợp, ta cần nhân đôi 1 Object để khi chỉnh sửa thằng này không ảnh hưởng đến thằng kia. Chúng ta gọi cách này là **Clone**
- Clone có 2 cách:
    - Clone thường (hay gọi là shallow copy)
    - Clone sâu (hay gọi là deep copy)

##### Với thằng clone thường -- Dùng Spread Syntax
    let user = {
        name: 'Anh Khoa',
        age: 24
    }
    let user2 = { ...user }
    user2.name = 'Quoc Thang'

    console.log(user.name) // Anh Khoa
    console.log(user2.name) // Quoc Thang

Hoặc chúng ta sẽ xài vòng lăp.

    let user = {
        name: 'Anh Khoa',
        age: 24
    }
    let user2 = {}

    for (let key in user)
    {
        user2[key] = user[key]
    }
**Clone thường** chỉ hiệu quả với Object 1 cắp. Đối với trường hợp **Nest Object** chúng ta sẽ sử dụng **Deep Clone**
##### Với thằng Deep Clone
Trong ví dụ trên, ta thấy các thuộc tính trong biến user đếu là **tham trị**. Tuy nhiên trong trường hợp **Nest Object** thì các thuộc tính của nó có thể **tham chiếu** đến 1 object khác.

    let user = {
        name: 'Anh Khoa',
        size: {
            heigth: 170,
            weigth: 80
        }
    }
Bây giờ, mình không thể dùng **clone thường** để copy Object do user.size này nó là 1 Object, nếu copy thì nó sẽ bị **tham chiếu** do đó, user.size và clone.size sẽ cùng tham chiếu đến 1 ô nhớ.
- Để xử lý thằng này, chúng ta sẽ có 1 số phương pháp:
    - Sử dụng JSON.parse(JSON.stringtify()) -- Tạo ra 1 Object mới.
    - Dùng method **_.cloneDeep(obj)**
    - Dùng các thư viện như **immer**.Thằng này hiệu quả khi chúng ta không cần thiết phải clone hết 1 obj lớn để chỉnh sửa 1 vài thuộc tính, cơ chế của thằng này là chỉnh sửa thuộc tính nào thì nó tự tính và clone cho đúng thôi. Vậy nên sẽ cải thiện về mặt **Performance** trong 1 số trường hợp.

## Lưu ý: Const Object vẫn có thể chỉnh sửa :)))