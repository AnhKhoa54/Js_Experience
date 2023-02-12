# Destructuring
- Là một cú pháp của JS cho phép lấy giá trị từ một Object hoặc Array để gán vào 1 biến khác
- Đối với Object, chúng ta không được gán trực tiếp vào 1 biến mới mà phải sử dụng cú pháp: 
    - **key : newName**
- Đối với Array, chúng ta có thể gán trực tiếp vào 1 biến mới.
#### Destructuring With Object
    let me = {
        name: 'Anh Khoa',
        age: 24,
        interest: 'running'
    }

    let { name: myName, age: myAge, interset: myInterst } = me
    console.log(myName) // Anh Khoa
#### Destructuring With Array
    let me = [
        'Anh Khoa',
        function(a, b) {
            return a + b
        }
    ]

    let data = [ name, age]
    console.log(name, age(20,4)) // Anh Khoa 24

# Spread Syntax
- Spread Syntax hay còn được gọi là three dot(...)
- Có thể phân rã một mảng/ object thành một chuỗi các tham số được phân tách bằng dấu phẩy ????? :). Theo mình hiểu thì nó có thể lấy ruột của thằng này copy ra tạo thành ruột của 1 thằng khác: **Shalow Copy**
- Cái Shallow Copy này sẽ tạo ra 1 thằng mới khác với thằng cũ (Không bằng nhau) nhưng các phần tử trong nó có thể bằng nhau
#### Spread With Object
    const originalObject = { enabled: true, darkMode: false }
    const secondObject = { ...originalObject }

    console.log(secondObject);//{enabled: true, darkMode: false}
#### Spread With Array
    const tools = ['hammer', 'screwdriver']
    const otherTools = ['wrench', 'saw']
    const allTools = [...tools, ...otherTools]

    console.log(allTools) 
    // ['hammer', 'screwdriver', 'wrench', 'saw']

# Rest Parameter
Hiểu nôm na là những tham số còn lại

    let data = [1,2,3,4,5,6]
    let [a, b, ...c] = data
    console.log(c) // [3,4,5,6]

    const handle = ({ a, b, ...c }) => {
        return c
    }
    const value = handle({ a: 1, b: 2, c: 3, d: 4, e: 5 })
    console.log(value) // { c: 3, d: 4, e: 5 }

# Tổng kết
- Destructuring dùng để tạo ra một new variable từ array item hoặc object property
- Spread Syntax dùng để unpack terables của một array, object hay function call
- Rest Parameter dùng để tạo ra một 1 array/ object từ 1 số lượng giá trị không xác định 