# Toán tử Logic và Template String

## Toán tử Logic
- Dựa trên **Truthy** và **Falsy**. Hay còn gọi là **Đúng** hoặc **Sai**
- Ngoài những giá trị sau thì tất cả đều đúng: 
    - False
    - 0
    - 0n
    - undefined
    - null
    - ''
    - NaN

## Toán tử 3 ngôi
    let name = 'Anh Khoa'
    name === 'Anh Khoa' ? console.log(true) : console.log(false) // True

## Optional Chaining ?.
Thông thường, khi chúng ta cố truy cập vào 1 thuộc tính **null** hoặc **undefined** thì sẽ xảy ra lỗi
Những lúc này thường sẽ dùng điều kiện để check trước

    let user = {}
    user.address ? alert(user.address.name) : alert (undefined) // undefined

Hoặc chúng ta có thể sử dụn cách gọn hơn:

    let user = {}
    alert(user?.address?.name) // undefined

- Nếu gặp giá trị **null** hay **undefined** nó sẽ trả về **undefined** ngay lập tức.

## Toán tử nullist ??
Dùng trong trường hợp check 1 giá trị có phải là **null** hay **undefined** hay không

    let user
    alert (user ?? 'Anonymous) // Anonymous (do user null)

## Template String
    let user1 = `string 1`
    let user2 = `
        string 3
        string 4
    `
    let c = `${user1} ${user2}`
    console.log(c)
    // string 1
            string 3
            string 4
            
- Sủ dụng `` để khai báo
- Có thể khai báo biến trong String.


