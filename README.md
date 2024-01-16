# Mediator Pattern in C#

## Introduction
The Mediator Pattern is a behavioral design pattern that allows us to reduce the complexity of communication between multiple objects or classes. This pattern provides a mediator class that normally handles all the communications between different classes and supports easy maintenance of the code by helping to reduce the coupling.

## Purpose
The main purpose of the Mediator Pattern is to control how objects interact with each other. Instead of classes communicating directly, and thus being tightly coupled, they communicate indirectly through a mediator. This makes the classes more reusable and the architecture more maintainable.

## Use Case in C#
In C#, the Mediator Pattern is particularly useful in scenarios where a system has multiple components interacting with each other, like in a GUI application with multiple UI elements, or in a system where multiple services need to interact.

## Example
Below is a simple example of the Mediator Pattern in C#:

### Mediator Interface
```csharp
public interface IMediator
{
    void SendMessage(string message, Colleague colleague);
}
```

### Concrete Mediator
```csharp
public class ConcreteMediator : IMediator
{
    public Colleague1 Colleague1 { get; set; }
    public Colleague2 Colleague2 { get; set; }

    public void SendMessage(string message, Colleague colleague)
    {
        if (colleague == Colleague1)
        {
            Colleague2.Notify(message);
        }
        else
        {
            Colleague1.Notify(message);
        }
    }
}
```

### Colleague Abstract Class
```csharp
public abstract class Colleague
{
    protected IMediator mediator;

    public Colleague(IMediator mediator)
    {
        this.mediator = mediator;
    }

    public abstract void Notify(string message);
}
```

### Concrete Colleagues
```csharp
public class Colleague1 : Colleague
{
    public Colleague1(IMediator mediator) : base(mediator) {}

    public override void Notify(string message)
    {
        Console.WriteLine("Colleague1 gets message: " + message);
    }
}

public class Colleague2 : Colleague
{
    public Colleague2(IMediator mediator) : base(mediator) {}

    public override void Notify(string message)
    {
        Console.WriteLine("Colleague2 gets message: " + message);
    }
}
```

### Usage
```csharp
var mediator = new ConcreteMediator();

var colleague1 = new Colleague1(mediator);
var colleague2 = new Colleague2(mediator);

mediator.Colleague1 = colleague1;
mediator.Colleague2 = colleague2;

colleague1.Send("Hello, World!"); // Colleague2 gets message: Hello, World!
colleague2.Send("Hi there!"); // Colleague1 gets message: Hi there!
```
