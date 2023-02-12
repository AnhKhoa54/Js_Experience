# ES6 Class
- Theo như mình tìm hiểu, trước ES6 thì javaScript không hỗ trợ **Class**
- Bài này mình không đi quá sâu vào ES6 Class, bởi vì mình không rành về nó và cũng không muốn tìm hiểu quá sâu vào nó. Nếu sau này trong công việc có nhu cầu đào sâu thêm mình sẽ tìm hiểu thêm.

## Constructor Function
    function Cat(name, color, type) {
        this.name = name,
        this.color = color,
        this.type = type
    }

    // Thêm một Method (Dùng Prototype để thêm)
    Cat.prototype.meow = function () {
        console.log(`${this.name} meows: meow meow meow!`)
    }

    // Khởi tạo 1 instance Object
    let alex = new Cat('Alex', 'White', 'Bengal')

    alex.meow() // Alex meows: meow meow meow!

Hoặc có thể dùng cách khác, thay vì dùng prototype để tạo Method thì có thể di chuyển cá method đó vào function luôn

    function Cat(name, color, type) {
        this.name = name,
        this.color = color,
        this.type = type
        this.meow = function () {
            console.log(`${this.name} meows: meow meow meow!`)
        }
    }


    // Khởi tạo 1 instance Object
    let alex = new Cat('Alex', 'White', 'Bengal')

    alex.meow() // Alex meows: meow meow meow!

## Class
Class giúp gom các thuộc tính và phương thức lại, giúp code nhìn clean hơn
Trong Class chỉ có thể khai báo Constructor và các Method, không thể khai báo biến trong đó

    class Cat {
        constructor(name, color, type) {
            // Tạo ra các thuộc tính (Property)
            this.name = name
            this.color color
            this.type = type
        }

        // Thêm vào các Method
        meow() {
            console.log(`${this.name} meows: meow meow meow!`)
        }
    }
    
    let alex = new Cat('Alex', 'White', 'Bengal')
    alex.meow() // Alex meows: meow meow meow!

##### Vấn đề this trong Class
    funtion handle(cb) {
        cb()
    }

    class Cat {
        constructor(name, color, type) {
            // Tạo ra các thuộc tính (Property)
            this.name = name
            this.color color
            this.type = type
        }

        // Thêm vào các Method
        meow() {
            console.log(`${this.name} meows: meow meow meow!`)
        }

        run() {
            handle(this.meow)
        }
    }
    
    let alex = new Cat('Alex', 'White', 'Bengal')

    alex.run() 
    // Uncaugth TypeError: Cannot reaf properties of undefined (reading'name')

Hiểu đơn giản là cái function handle() nó nằm ngoài thằng Cat, do đó nó không hiểu được cái giá trị **this** truyền vào

Cách fix 1: Dùng **bind()**

    funtion handle(cb) {
        cb()
    }

    class Cat {
        constructor(name, color, type) {
            // Tạo ra các thuộc tính (Property)
            this.name = name
            this.color color
            this.type = type
            this.meow = this.meow.bind(this)
        }

        // Thêm vào các Method
        meow() {
            console.log(`${this.name} meows: meow meow meow!`)
        }

        run() {
            handle(this.meow)
        }
    }
    
    let alex = new Cat('Alex', 'White', 'Bengal')

    alex.run() // Alex meows: meow meow meow!

Cách Fix 2: Dùng arrow function cho method **meow**

    funtion handle(cb) {
        cb()
    }

    class Cat {
        constructor(name, color, type) {
            // Tạo ra các thuộc tính (Property)
            this.name = name
            this.color color
            this.type = type
        }

        meow = () => {
            console.log(`${this.name} meows: meow meow meow!`)
        }

        run() {
            handle(this.meow)
        }
    }
    
    let alex = new Cat('Alex', 'White', 'Bengal')

    alex.run() // Alex meows: meow meow meow!

Cách Fix 3: Dùng Arrow Function cho callback lúc truyền vào function

    funtion handle(cb) {
        cb()
    }

    class Cat {
        constructor(name, color, type) {
            // Tạo ra các thuộc tính (Property)
            this.name = name
            this.color color
            this.type = type
        }

        meow() {
            console.log(`${this.name} meows: meow meow meow!`)
        }

        run() {
            handle(() => { this.meow})
        }
    }
    
    let alex = new Cat('Alex', 'White', 'Bengal')

    alex.run() // Alex meows: meow meow meow!