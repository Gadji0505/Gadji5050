import java.util.Scanner;

public class AbstractClass {
    public static void main(String[]args){

        Scanner myScanner = new Scanner(System.in);
        System.out.println("Укажите колличество фигур ");

        Body []myBody = new Body [myScanner.nextInt()];

        for(int i=0;i<myBody.length;i++){
            System.out.println("Шар - 1  или Параллелепипед - 2");
            if(myScanner.nextInt()==1){
                System.out.println("Укажите радиус окружности ");
                myBody[i]=new Sphere(myScanner.nextInt());
            }else{
                System.out.println("Укажите укажите размер параллелепипеда ");
                myBody[i]=new Parallelepiped(myScanner.nextInt(),myScanner.nextInt(),myScanner.nextInt());
            }
        }

        for(Body b:myBody){
            b.print();
        }

    }
}





abstract public class Body {

abstract double square();
abstract double volume();
abstract void print();

}





public class Parallelepiped extends Body{
    private double a,b,c;

    Parallelepiped(int a, int b, int c){
        this.a=a;
        this.b=b;
        this.c=c;
    }

    @Override
    double square() {
        return 2*(a*b+a*c+b*c);
    }

    @Override
    double volume() {
        return a*b*c;
    }

    @Override
    void print() {
        System.out.println(
                "Размеры сторон: "+
                        "\nСторона а = "+a+
                        "\nСторона b = "+b+
                        "\nСторона c = "+c+
                        "\nОбъём = "+this.volume()+"\nПлощадь = "+this.square()
        );

    }



}






public class Sphere extends Body{
    private double radius;

    Sphere(int radius){
        this.radius=radius;
    }
    @Override
    double square() {
        return Math.PI * Math.pow(radius,2);
    }

    @Override
    double volume() {
        return 4*Math.PI*Math.pow(radius,3)/3;
    }

    @Override
    void print() {
        System.out.println("" +
                "Радиус шара = "+ radius+"" +
                "\nОбъём ="+this.volume()+"\nПлощадь ="+this.square());
    }

}