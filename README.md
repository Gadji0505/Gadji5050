import java.util.Scanner;

// Основной класс
public class AbstractClass {
    public static void main(String[] args) {
        Scanner myScanner = new Scanner(System.in);
        System.out.println("Укажите количество фигур: ");
        
        Body[] myBody = new Body[myScanner.nextInt()];

        for (int i = 0; i < myBody.length; i++) {
            System.out.println("Треугольник - 1 или Окружность - 2");
            if (myScanner.nextInt() == 1) {
                System.out.println("Укажите длины сторон треугольника (a, b, c): ");
                double a = myScanner.nextDouble();
                double b = myScanner.nextDouble();
                double c = myScanner.nextDouble();
                myBody[i] = new Triangle(a, b, c);
            } else {
                System.out.println("Укажите радиус окружности: ");
                myBody[i] = new Circle(myScanner.nextDouble());
            }
        }

        for (Body b : myBody) {
            b.print();
        }
    }
}

// Абстрактный класс
abstract public class Body {
    abstract double square();   // метод для вычисления площади
    abstract double perimeter(); // метод для вычисления периметра
    abstract void print();       // метод для вывода информации
}

// Класс Треугольник
public class Triangle extends Body {
    private double a, b, c;

    Triangle(double a, double b, double c) {
        this.a = a;
        this.b = b;
        this.c = c;
    }

    @Override
    double square() {
        double s = (a + b + c) / 2; // полупериметр
        return Math.sqrt(s * (s - a) * (s - b) * (s - c)); // формула Герона
    }

    @Override
    double perimeter() {
        return a + b + c; // периметр
    }

    @Override
    void print() {
        System.out.println("Стороны треугольника: a = " + a + ", b = " + b + ", c = " + c +
                           "\nПлощадь = " + this.square() + "\nПериметр = " + this.perimeter());
    }
}

// Класс Окружность
public class Circle extends Body {
    private double radius;

    Circle(double radius) {
        this.radius = radius;
    }

    @Override
    double square() {
        return Math.PI * Math.pow(radius, 2); // площадь круга
    }

    @Override
    double perimeter() {
        return 2 * Math.PI * radius; // длина окружности
    }

    @Override
    void print() {
        System.out.println("Радиус окружности = " + radius + 
                           "\nПлощадь = " + this.square() + 
                           "\nПериметр (длина окружности) = " + this.perimeter());
    }
}