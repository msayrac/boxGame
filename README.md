# boxGame

# Main.java

import java.sql.SQLOutput;

public class Main {

    public static void main(String[] args) {

        Fighter f1 = new Fighter("A",10,120,100,30);
        Fighter f2= new Fighter("B",20,85,85,40);

        Match match = new Match(f1,f2,85,100);

        match.run();

    }
}


# Fighter.java
public class Fighter {

    String name;
    int damage;
    int health;
    int weight;

    int dodge;


    Fighter(String name,int damage, int health, int weight, int dodge){
        this.name=name;
        this.damage=damage;
        this.health=health;
        this.weight=weight;
        if(dodge>=0 && dodge<=100){
            this.dodge=dodge;
        } else{
            this.dodge=0;
        }
    }

    int hit(Fighter foe){
        System.out.println(this.name + " => "+foe.name+ " "+ this.damage +" hasar vurdu.");
        if(foe.isDodge()){
            System.out.println(foe.name +" gelen hasari blokladi!" );
            return foe.health;
        }
        if(foe.health-this.damage<0){
            return 0;
        }
        return foe.health-this.damage;
    }

    boolean isDodge(){

        double randomNumber = Math.random()*100;
        return randomNumber<=this.dodge;
    }
}

# Match.java
public class Match {
    Fighter f1;
    Fighter f2;

    int minWeight;
    int maxWeight;

    Match(Fighter f1, Fighter f2, int minWeight, int maxWeight) {
        this.f1 = f1;
        this.f2=f2;
        this.minWeight=minWeight;
        this.maxWeight=maxWeight;

    }

    public void run(){
        if(isCheck()){


            while(this.f1.health>0 && this.f2.health>0){
                System.out.println("====Yeni Round ====== ");

                if(first()==1){
                    this.f2.health = this.f1.hit(this.f2);
                    //System.out.println(this.f2.health);
                    if(isWin()){
                        break;
                    }

                    this.f1.health=this.f2.hit(this.f1);
                    // System.out.println(this.f1.health);
                    if(isWin()){
                        break;
                    }

                } else{



                    this.f1.health = this.f2.hit(this.f1);
                    if(isWin()){
                        break;
                    }

                    this.f2.health=this.f1.hit(this.f2);
                    if(isWin()){
                        break;
                    }



                }

                System.out.println(this.f1.name + " saglik : "+ this.f1.health);
                System.out.println(this.f2.name + " saglik : "+ this.f2.health);
            }


        } else{
            System.out.println("Sporcular skiletleri uymuyor.");
        }
    }

    boolean isCheck(){
        return(this.f1.weight>=minWeight && this.f1.weight<=maxWeight)&&(this.f2.weight>=minWeight&&this.f2.weight<=maxWeight);
    }

    boolean isWin(){


        if(this.f1.health==0){
            System.out.println(this.f2.name + " kazandi !");
            return true;
        }
        if(this.f2.health==0){
            System.out.println(this.f1.name + " kazandi !");
            return true;

        }
        return false;
    }

    int first(){
        double firstOne=Math.random()*100;
        if(firstOne<50){
            return 1;
        } else{
            return 0;
        }
    }

}


