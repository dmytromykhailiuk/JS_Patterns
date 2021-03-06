# DESIGN PATTERNS :see_no_evil:

<b>Design patterns</b> are typical solutions to commonly occurring problems in software design. They are like pre-made blueprints that you can customize to solve a recurring design problem in your code.

You can’t just find a pattern and copy it into your program, the way you can with off-the-shelf functions or libraries. The pattern is not a specific piece of code, but a general concept for solving a particular problem. You can follow the pattern details and implement a solution that suits the realities of your own program.

Patterns are often confused with algorithms, because both concepts describe typical solutions to some known problems. While an algorithm always defines a clear set of actions that can achieve some goal, a pattern is a more high-level description of a solution. The code of the same pattern applied to two different programs may be different.

An analogy to an algorithm is a cooking recipe: both have clear steps to achieve a goal. On the other hand, a pattern is more like a blueprint: you can see what the result and its features are, but the exact order of implementation is up to you.

<hr/>

## Creational patterns :cactus:
These patterns provide various object creation mechanisms, which increase flexibility and reuse of existing code.

### Abstract Factory :wrench:
```
Abstract Factory is a creational design pattern that lets you produce 
families of related objects without specifying their concrete classes.
```
<details><summary><b>JavaScript Example</b></summary>
<p>
    
```js
function bmwProducer(kind) {
  return kind === 'sport' ? sportCarFactory : familyCarFactory;
}

function sportCarFactory() {
	return new Z4();
}

function familyCarFactory() {
	return new I3();
}

class Z4 {
	info() {
		return "Z4 is a Sport car!";
	}
}

class I3 {
	info() {
		return "i3 is a Family car!";
	}
}

const produce = bmwProducer('sport');

const myCar = new produce();

console.log(myCar.info());
```
</p>
</details>

### Factory method :wrench:
```
Factory Method is a creational design pattern that provides an interface 
for creating objects in a superclass, but allows subclasses to alter the 
type of objects that will be created.
```
<details><summary><b>JavaScript Example</b></summary>
<p>
    
```js
class Bmw {
  constructor(model, price, maxSpeed) {
    this.model = model;
    this.price = price;
    this.maxSpeed = maxSpeed;
  }
}

class BmwFactory {
  static create(type) {
    if (type === "X5") return new Bmw(type, 108000, 300);
    if (type === "X6") return new Bmw(type, 111000, 320);
  }
}

const x5 = BmwFactory.create("X5");
const x6 = BmwFactory.create("X6");

console.log(x5);

console.log(x6);
```
</p>
</details>

### Builder :wrench:
```
Builder is a creational design pattern that lets you construct complex 
objects step by step. The pattern allows you to produce different 
types and representations of an object using the same construction code.
```
<details><summary><b>JavaScript Example</b></summary>
<p>
    
```js
class Car {
  constructor() {
    this.autoPilot = false;
    this.parktronic = false;
    this.signaling = false;
  }
}

class CarBuilder {
  constructor() {
    this.car = new Car();
  }

  addAutoPilot(autoPilot) {
    this.car.autoPilot = autoPilot;
    return this;
  }

  addParktronic(parktronic) {
    this.car.parktronic = parktronic;
    return this;
  }

  addSignaling(signaling) {
    this.car.signaling = signaling;
    return this;
  }

  updateEngine(engine) {
    this.car.engine = engine;
    return this;
  }

  build() {
    return this.car;
  }
}

const newCar = new CarBuilder()
  .addAutoPilot("someAutoPilot")
  .addParktronic("someParktronic")
  .build();
console.log(newCar); // { autoPilot: undefined, parktronic: undefined, signaling: false }
```
</p>
</details>

### Prototype :wrench:
```
Prototype is a creational design pattern that lets you copy 
existing objects without making your code dependent on their 
classes.
```
<details><summary><b>JavaScript Example</b></summary>
<p>
    
```js
class TeslaCar {
  constructor(model, price, interior, autopilot) {
    this.model = model;
    this.price = price;
    this.interior = interior;
    this.autopilot = autopilot;
  }

  produce() {
    return new TeslaCar(this.model, this.price, this.interior, this.autopilot);
  }
}

const tesla1 = new TeslaCar("S", 50000, false, false);
const tesla1Clone = tesla1.produce();

console.log(tesla1, tesla1Clone);
```
</p>
</details>

### Singleton :wrench:
```
Singleton is a creational design pattern that lets you ensure that 
a class has only one instance, while providing a global access 
point to this instance.
```
<details><summary><b>JavaScript Example</b></summary>
<p>
    
```js
const Counter = (() => {
  let instance = null;
  count = 0;
  return class {
    constructor() {
      if (instance) {
        return instance;
      }
      this.count = 0;
      instance = this;
      return this;
    }

    getCount() {
      return this.count;
    }

    increaseCount() {
      return this.count++;
    }
  };
})();

const myCount1 = new Counter();

myCount1.increaseCount();
myCount1.increaseCount();
myCount1.increaseCount();
myCount1.increaseCount();

const myCount2 = new Counter();

console.log(myCount2.getCount());

myCount2.increaseCount();
myCount2.increaseCount();

console.log(myCount1.getCount());
```
</p>
</details>

<hr/>

## Structural Patterns :cactus:
Structural patterns explain how to assemble objects and classes into larger structures while keeping these structures flexible and efficient.

### Adapter :wrench:
```
Adapter is a structural design pattern that allows objects with 
incompatible interfaces to collaborate.
```
<details><summary><b>JavaScript Example</b></summary>
<p>
    
```js
class Engine2 {
  simpleInterface() {
    console.log("Engine 2.0 - tr-tr-tr");
  }
}

class EngineV8 {
  complecatedInterface() {
    console.log("Engine V8! - wroom wroom!");
  }
}

class EngineV8Adapter {
  constructor(engine) {
    this.engine = engine;
  }

  simpleInterface() {
    this.engine.complecatedInterface();
  }
}

class Auto {
  startEngine(engine) {
    engine.simpleInterface();
  }
}

const auto = new Auto();
auto.startEngine(new Engine2()); // Engine 2.0 - tr-tr-tr

auto.startEngine(new EngineV8Adapter(new EngineV8())); // Engine V8! - wroom wroom!
```
</p>
</details>

### Bridge :wrench:
```
Bridge is a structural design pattern that lets you split a large 
class or a set of closely related classes into two separate 
hierarchies—abstraction and implementation—which can be developed 
independently of each other.
```
<details><summary><b>JavaScript Example</b></summary>
<p>
    
```js
class Model {
  constructor(color) {
    this.color = color;
  }
}

class Color {
  constructor(type) {
    this.type = type;
  }
  get() {
    return this.type;
  }
}

class BlackColor extends Color {
  constructor() {
    super("dark-black");
  }
}

class SilbrigColor extends Color {
  constructor() {
    super("Silbermetallic");
  }
}

class Audi extends Model {
  constructor(color) {
    super(color);
  }

  paint() {
    return `Auto: Audi, Color: ${this.color.get()}`;
  }
}

class Bmw extends Model {
  constructor(color) {
    super(color);
  }

  paint() {
    return `Auto: Bmw, Color: ${this.color.get()}`;
  }
}

const blackBmw = new Bmw(new BlackColor());
console.log(blackBmw.paint());
```
</p>
</details>

### Composite :wrench:
```
Composite is a structural design pattern that lets you compose 
objects into tree structures and then work with these structures 
as if they were individual objects.
```
<details><summary><b>JavaScript Example</b></summary>
<p>
    
```js
class Equipment {
	getPrice() {
		return this.price || 0;
	}

	getName() {
		return this.name;
	}

	setName(name) {
		this.name = name;
	}

	setPrice(price) {
		this.price = price;
	}
}

class Engine extends Equipment {
	constructor() {
		super();
		this.setName('Engine');
		this.setPrice(800);
	}
}

class Body extends Equipment {
	constructor() {
		super();
		this.setName('Body');
		this.setPrice(3000);
	}
}

class Tools extends Equipment {
	constructor() {
		super();
		this.setName('Tools');
		this.setPrice(4000);
	}
}

class Composite extends Equipment {
	constructor() {
		super();
		this.equipments = [];
	}

	add(equipment) {
		this.equipments.push(equipment);
	}

	getPrice() {
		return this.equipments
			.map(equipment => equipment.getPrice())
			.reduce((a, b) => a + b);
	}
}

class Car extends Composite {
	constructor() {
		super();
		this.setName('Audi');
	}
}

const myCar = new Car();

myCar.add(new Engine());
myCar.add(new Body());
myCar.add(new Tools());

console.log(`${myCar.getName()} price is ${myCar.getPrice()}`);
```
</p>
</details>

### Decorator :wrench:
```
Decorator is a structural design pattern that lets you attach 
new behaviors to objects by placing these objects inside special 
wrapper objects that contain the behaviors.
```
<details><summary><b>JavaScript Example</b></summary>
<p>
    
```js
class Car {
  constructor() {
    this.price = 10000;
    this.model = "Car";
  }

  getPrice() {
    return this.price;
  }

  getDescription() {
    return this.model;
  }
}

class Tesla extends Car {
  constructor() {
    super();
    this.price = 25000;
    this.model = "Tesla";
  }
}

class Autopilot {
  constructor(car) {
    this.car = car;
  }

  getPrice() {
    return this.car.getPrice() + 5000;
  }

  getDescription() {
    return `${this.car.getDescription()} with autopilot`;
  }
}

class Parktronic {
  constructor(car) {
    this.car = car;
  }

  getPrice() {
    return this.car.getPrice() + 3000;
  }

  getDescription() {
    return `${this.car.getDescription()} with parktronic`;
  }
}

let tesla1 = new Tesla();
tesla1 = new Autopilot(tesla1);
tesla1 = new Parktronic(tesla1);
console.log(tesla1.getPrice(), tesla1.getDescription()); // 33000 Tesla with autopilot with parktronic

let tesla2 = new Tesla();
tesla2 = new Autopilot(tesla2);
console.log(tesla2.getPrice(), tesla2.getDescription()); // 30000 Tesla with autopilot
```
</p>
</details>

### Facade :wrench:
```
Facade is a structural design pattern that provides a simplified 
interface to a library, a framework, or any other complex set of 
classes.
```
<details><summary><b>JavaScript Example</b></summary>
<p>
    
```js
class Сonveyor {
  setBody() {
    console.log("Body set!");
  }

  getEngine() {
    console.log("Dismantle Engine!");
  }

  setEngine() {
    console.log("Engine set!");
  }

  getInterior() {
    console.log("Dismantle Exterior!");
  }

  setInterior() {
    console.log("Exterior added!");
  }

  changeInterior() {
    console.log("Update interior!");
  }

  setExterior() {
    console.log("Added interior!");
  }

  setWheels() {
    console.log("Wheels!");
  }

  addElectronics() {
    console.log("Added electronics!");
  }

  paint() {
    console.log("Car painted!");
  }
}

class СonveyorFacade {
  constructor(car) {
    this.car = car;
  }

  assembleCar() {
    this.car.setBody();
    this.car.setEngine();
    this.car.setInterior();
    this.car.setExterior();
    this.car.setWheels();
    this.car.addElectronics();
    this.car.paint();
  }

  changeEngine() {
    this.car.getEngine();
    this.car.setEngine();
  }

  changeInterior() {
    this.car.getInterior();
    this.car.setInterior();
  }
}

const conveyor = new СonveyorFacade(new Сonveyor());

let car = conveyor.assembleCar();
console.log();

car = conveyor.changeEngine();
console.log();

car = conveyor.changeInterior();
```
</p>
</details>

### Flyweight :wrench:
```
Flyweight is a structural design pattern that lets you fit more 
objects into the available amount of RAM by sharing common parts 
of state between multiple objects instead of keeping all of the 
data in each object.
```
<details><summary><b>JavaScript Example</b></summary>
<p>
    
```js
class Auto {
  constructor(model) {
    this.model = model;
  }
}

class AutoFactory {
  constructor() {
    this.models = {};
  }

  create(name) {
    let model = this.models[name];
    if (model) return model;
    this.models[name] = new Auto(name);
    return this.models[name];
  }
}

const factory = new AutoFactory();

const bmw = factory.create("BMW");
const bmw2 = factory.create("BMW");
const audi = factory.create("AUDI");
const tesla = factory.create("TESLA");
const tesla2 = factory.create("TESLA");

console.log(factory.models);
```
</p>
</details>

### Proxy :wrench:
```
Proxy is a structural design pattern that lets you provide a substitute 
or placeholder for another object. A proxy controls access to the 
original object, allowing you to perform something either before or 
after the request gets through to the original object.
```
<details><summary><b>JavaScript Example</b></summary>
<p>
    
```js
class CarAccess {
  open() {
    console.log("Opening car door");
  }

  close() {
    console.log("Closing the car door");
  }
}

class SecuritySystem {
  constructor(door) {
    this.door = door;
  }

  open(password) {
    if (this.authenticate(password)) {
      this.door.open();
    } else {
      console.log("Access denied!");
    }
  }

  authenticate(password) {
    return password === "Ilon";
  }

  close() {
    this.door.close();
  }
}

const door = new SecuritySystem(new CarAccess());

door.open("Jack");

door.open("Ilon");

door.close();
```
</p>
</details>

<hr/>

## Behavioral Patterns :cactus:
Behavioral design patterns are concerned with algorithms and the assignment of responsibilities between objects.

### Chain of Responsibility :wrench:
```
Chain of Responsibility is a behavioral design pattern that lets 
you pass requests along a chain of handlers. Upon receiving a 
request, each handler decides either to process the request or 
to pass it to the next handler in the chain.
```
<details><summary><b>JavaScript Example</b></summary>
<p>
    
```js
class MySum {
  constructor(initialValue = 42) {
    this.sum = initialValue;
  }

  add(value) {
    this.sum += value;
    return this;
  }
}

const sum1 = new MySum();
console.log(sum1.add(8).add(10).add(1).add(9).sum);

const sum2 = new MySum(0);
console.log(sum2.add(1).add(2).add(3).sum);
```
</p>
</details>

### Command :wrench:
```
Command is a behavioral design pattern that turns a request into a 
stand-alone object that contains all information about the request. 
This transformation lets you parameterize methods with different 
requests, delay or queue a request’s execution, and support undoable 
operations.
```
<details><summary><b>JavaScript Example</b></summary>
<p>
    
```js
class MyMath {
  constructor(initialValue = 0) {
    this.num = initialValue;
  }

  square() {
    return this.num ** 2;
  }

  cube() {
    return this.num ** 3;
  }
}

class Command {
  constructor(subject) {
    this.subject = subject;
    this.commandsExecuted = [];
  }

  execute(command) {
    this.commandsExecuted.push(command);
    return this.subject[command]();
  }
}

const x = new Command(new MyMath(2));

console.log(x.execute("square"));
console.log(x.execute("cube"));

console.log(x.commandsExecuted);
```
</p>
</details>

### Iterator :wrench:
```
Iterator is a behavioral design pattern that lets you traverse 
elements of a collection without exposing its underlying 
representation (list, stack, tree, etc.).
```
<details><summary><b>JavaScript Example</b></summary>
<p>
    
```js
class ArrayIterator {
  constructor(el) {
    this.index = 0;
    this.elements = el;
  }

  next() {
    return this.elements[this.index++];
  }

  hasNext() {
    return this.index < this.elements.length;
  }
}

const autos1 = [
  { model: "Audi", color: "black", price: "20000" },
  { model: "BMW", color: "white", price: "30000" },
  { model: "Tesla", color: "gray", price: "40000" },
];

const collection1 = new ArrayIterator(autos1);

while (collection1.hasNext()) {
  console.log(collection1.next());
}

class ObjectIterator {
  constructor(el) {
    this.index = 0;
    this.keys = Object.keys(el);
    this.elements = el;
  }

  next() {
    return this.elements[this.keys[this.index++]];
  }

  hasNext() {
    return this.index < this.keys.length;
  }
}

const autos2 = {
  audi: { model: "Audi", color: "black", price: "20000" },
  bmw: { model: "BMW", color: "white", price: "30000" },
  tesla: { model: "Tesla", color: "gray", price: "40000" },
};

const collection2 = new ObjectIterator(autos2);

while (collection2.hasNext()) {
  console.log(collection2.next());
}
```
</p>
</details>

### Mediator :wrench:
```
Mediator is a behavioral design pattern that lets you reduce chaotic 
dependencies between objects. The pattern restricts direct communications 
between the objects and forces them to collaborate only via a mediator 
object.
```
<details><summary><b>JavaScript Example</b></summary>
<p>
    
```js
class User {
  constructor(name) {
    this.name = name;
    this.room = null;
  }

  send(message, to) {
    this.room.send(message, this, to);
  }

  receive(message, from) {
    console.log(`${from.name} => ${this.name}: ${message}`);
  }
}

class ChatRoom {
  constructor() {
    this.users = {};
  }

  register(user) {
    this.users[user.name] = user;
    user.room = this;
  }

  send(message, from, to) {
    if (to) {
      to.receive(message, from);
    } else {
      Object.keys(this.users).forEach((key) => {
        if (this.users[key] !== from) {
          this.users[key].receive(message, from);
        }
      });
    }
  }
}

const vlad = new User("Vladilen");
const lena = new User("Elena");
const igor = new User("Igor");

const room = new ChatRoom();

room.register(vlad);
room.register(lena);
room.register(igor);

vlad.send("Hello!", lena);
lena.send("Hello hello!", vlad);
igor.send("Vsem privet");
```
</p>
</details>

### Memento :wrench:
```
Memento is a behavioral design pattern that lets you save and restore 
the previous state of an object without revealing the details of its 
implementation.
```
<details><summary><b>JavaScript Example</b></summary>
<p>
    
```js
class Memento {
  constructor(value) {
    this.value = value;
  }
}

const creator = {
  save: (val) => new Memento(val),
  restore: (memento) => memento.value,
};

class Caretaker {
  constructor() {
    this.values = [];
  }

  addMemento(memento) {
    this.values.push(memento);
  }

  getMemento(index) {
    return this.values[index];
  }
}

const careTaker = new Caretaker();

careTaker.addMemento(creator.save("hello"));
careTaker.addMemento(creator.save("hello world"));
careTaker.addMemento(creator.save("hello world!!!"));

console.log(creator.restore(careTaker.getMemento(1)));
```
</p>
</details>

### Observer :wrench:
```
Observer is a behavioral design pattern that lets you define a subscription 
mechanism to notify multiple objects about any events that happen to the 
object they’re observing.
```
<details><summary><b>JavaScript Example</b></summary>
<p>
    
```js
class Subject {
  constructor() {
    this.observers = [];
  }

  subscribe(observer) {
    this.observers.push(observer);
  }

  unsubscribe(observer) {
    this.observers = this.observers.filter((obs) => obs !== observer);
  }

  fire(action) {
    this.observers.forEach((observer) => {
      observer.update(action);
    });
  }
}

class Observer {
  constructor(state = 1) {
    this.state = state;
    this.initialState = state;
  }

  update(action) {
    switch (action.type) {
      case "INCREMENT":
        this.state = ++this.state;
        break;
      case "DECREMENT":
        this.state = --this.state;
        break;
      case "ADD":
        this.state += action.payload;
        break;
      default:
        this.state = this.initialState;
    }
  }
}

const stream$ = new Subject();

const obs1 = new Observer();
const obs2 = new Observer(42);

stream$.subscribe(obs1);
stream$.subscribe(obs2);

stream$.fire({ type: "INCREMENT" });
stream$.fire({ type: "INCREMENT" });
stream$.fire({ type: "DECREMENT" });
stream$.fire({ type: "ADD", payload: 10 });

console.log(obs1.state);
console.log(obs2.state);
```
</p>
</details>

### State :wrench:
```
State is a behavioral design pattern that lets an object alter its 
behavior when its internal state changes. It appears as if the object 
changed its class.
```
<details><summary><b>JavaScript Example</b></summary>
<p>
    
```js
class Light {
  constructor(light) {
    this.light = light;
  }
}

class RedLight extends Light {
  constructor() {
    super("red");
  }

  sign() {
    return "STOP";
  }
}

class YellowLight extends Light {
  constructor() {
    super("yellow");
  }

  sign() {
    return "READY";
  }
}

class GreenLight extends Light {
  constructor() {
    super("green");
  }

  sign() {
    return "GO!";
  }
}

class TrafficLight {
  constructor() {
    this.states = [new RedLight(), new YellowLight(), new GreenLight()];
    this.current = this.states[0];
  }

  change() {
    const total = this.states.length;
    let index = this.states.findIndex((light) => light === this.current);

    if (index + 1 < total) {
      this.current = this.states[index + 1];
    } else {
      this.current = this.states[0];
    }
  }

  sign() {
    return this.current.sign();
  }
}

const traffic = new TrafficLight();
console.log(traffic.sign());
traffic.change();

console.log(traffic.sign());
traffic.change();

console.log(traffic.sign());
traffic.change();

console.log(traffic.sign());
traffic.change();

console.log(traffic.sign());
traffic.change();

console.log(traffic.sign());
traffic.change();

console.log(traffic.sign());
```
</p>
</details>

### Strategy :wrench:
```
Strategy is a behavioral design pattern that lets you define a family 
of algorithms, put each of them into a separate class, and make their 
objects interchangeable.
```
<details><summary><b>JavaScript Example</b></summary>
<p>
    
```js
function baseStrategy(amount) {
  return amount;
}

function premiumStrategy(amount) {
  return amount * 0.85;
}

function platinumStrategy(amount) {
  return amount * 0.65;
}

class AutoCart {
  constructor(discount) {
    this.discount = discount;
    this.amount = 0;
  }

  checkout() {
    return this.discount(this.amount);
  }

  setAmount(amount) {
    this.amount = amount;
  }
}

const baseCustomer = new AutoCart(baseStrategy);
const premiumCustomer = new AutoCart(premiumStrategy);
const platinumCustomer = new AutoCart(platinumStrategy);

baseCustomer.setAmount(50000);
console.log(baseCustomer.checkout()); // 50000

premiumCustomer.setAmount(50000);
console.log(premiumCustomer.checkout()); // 42500

platinumCustomer.setAmount(50000);
console.log(platinumCustomer.checkout()); // 32500
```
</p>
</details>

### Template Method :wrench:
```
Template Method is a behavioral design pattern that defines the skeleton of 
an algorithm in the superclass but lets subclasses override specific steps 
of the algorithm without changing its structure.
```
<details><summary><b>JavaScript Example</b></summary>
<p>
    
```js
class Employee {
  constructor(name, salary) {
    this.name = name;
    this.salary = salary;
  }

  responsibilities() {}

  work() {
    return `${this.name} выполняет ${this.responsibilities()}`;
  }

  getPaid() {
    return `${this.name} имеет ЗП ${this.salary}`;
  }
}

class Developer extends Employee {
  constructor(name, salary) {
    super(name, salary);
  }

  responsibilities() {
    return "процесс создания программ";
  }
}

class Tester extends Employee {
  constructor(name, salary) {
    super(name, salary);
  }

  responsibilities() {
    return "процесс тестирования";
  }
}

const dev = new Developer("Владилен", 100000);
console.log(dev.getPaid());
console.log(dev.work());

const tester = new Tester("Виктория", 90000);
console.log(tester.getPaid());
console.log(tester.work());
```
</p>
</details>

### Visitor :wrench:
```
Visitor is a behavioral design pattern that lets you separate
algorithms from the objects on which they operate.
```
<details><summary><b>JavaScript Example</b></summary>
<p>
    
```js
class Auto {
  accept(visitor) {
    visitor(this);
  }
}

class Tesla extends Auto {
  info() {
    return "It is a Tesla car!";
  }
}

class Bmw extends Auto {
  info() {
    return "It is a BMW car!";
  }
}

class Audi extends Auto {
  info() {
    return "It is an Audi car!";
  }
}

function exportVisitor(auto) {
  if (auto instanceof Tesla)
    auto.export = console.log(`Exported data: ${auto.info()}`);
  if (auto instanceof Bmw)
    auto.export = console.log(`Exported data: ${auto.info()}`);
  if (auto instanceof Audi)
    auto.export = console.log(`Exported data: ${auto.info()}`);
}

const tesla = new Tesla();
tesla.accept(exportVisitor); // Exported data: It is a Tesla car!

const bmv = new Bmw();
bmv.accept(exportVisitor); // Exported data: It is a BMW car!
```
</p>
</details>

<hr/>

### Want to know more?
### <a href="https://refactoring.guru/design-patterns">Follow the link...</a>
