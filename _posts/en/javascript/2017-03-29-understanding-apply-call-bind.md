**Call apply and bind. and how they are different.**

Lets learn call and apply using any daily terminology. 

You have three automobiles `your_scooter , your_car and your_jet` which start with the same mechanism (method). 
We created an object `automobile` with a method `push_button_engineStart`. 

    var your_scooter, your_car, your_jet;
    var automobile = {
    	    push_button_engineStart: function (runtime){
    		console.log(this.name + "'s" + ' engine_started, buckle up for the ride for ' + runtime + " minutes");
    	}
    }

Lets understand when is call and apply used. Lets suppose that you are an engineer and you have `your_scooter`, `your_car` and `your_jet` which did not come with a push_button_engine_start and you wish to use a third party `push_button_engineStart`.

If you run the following lines of code, they will give an error. WHY?

    //your_scooter.push_button_engineStart();
    //your_car.push_button_engineStart();
    //your_jet.push_button_engineStart();
    
    
    automobile.push_button_engineStart.apply(your_scooter,[20]);
    automobile.push_button_engineStart.call(your_jet,10);
    automobile.push_button_engineStart.call(your_car,40);

So the above example is successfully gives your_scooter, your_car, your_jet a feature from automobile object.
 
**Let's dive deeper**
Here we will split the above line of code. 
`automobile.push_button_engineStart` is helping us to get the method being used. 

Further we use apply or call using the dot notation. 
`automobile.push_button_engineStart.apply()`


Now apply and call accept two parameters. 


 1. context
 2. arguments

So here we set the context in the final line of code. 

`automobile.push_button_engineStart.apply(your_scooter,[20])`

**Difference between call and apply** is just that apply accepts parameters in the form of an array while call simply can accept a comma separated list of arguments. 


**what is JS Bind function?**


A bind function is basically which binds the context of something and then stores it into a variable for execution at a later stage. 

Let's make our previous example even better. Earlier we used a method belonging to the automobile object and used it to equip `your_car, your_jet and your_scooter`. Now lets imagine we want to give a separate `push_button_engineStart` separately to start our automobiles individually at any later stage of the execution we wish. 



    var scooty_engineStart = automobile.push_button_engineStart.bind(your_scooter);
    var car_engineStart = automobile.push_button_engineStart.bind(your_car);
    var jet_engineStart = automobile.push_button_engineStart.bind(your_jet);
    
    
    setTimeout(scooty_engineStart,5000,30);
    setTimeout(car_engineStart,10000,40);
    setTimeout(jet_engineStart,15000,5);

***still not satisfied?***

Let's make it clear as teardrop. Time to experiment. We will go back to call and apply function application and try storing the value of the function as a reference. 

The experiment below fails because call and apply are invoked immediately, hence, we never get to the stage of storing a reference in a variable which is where bind function steals the show


`var test_function = automobile.push_button_engineStart.apply(your_scooter);`













