- An observer is a class that is registered with a subject
- When the subject changes, the observer is notified and changes accordingly
- The observer is part of the MVC architectural pattern, as the ‘view’

%%[[Git Ignore/Heavy Stuff/Matthew Barnes Notes/Software Modelling and Design Notes.pdf#page=55&selection=20,0,28,69&color=yellow|Software Modelling and Design Notes, p.55]]%%

![[Images/Software Modelling and Design Notes 1.png]]

%%[[Git Ignore/Heavy Stuff/Matthew Barnes Notes/Software Modelling and Design Notes.pdf#page=56&rect=108,617,479,780&color=yellow|Software Modelling and Design Notes, p.56]]%%

# Example Implementation & Components

- *Subject*
	- Maintains a list of observers (subscribers or listeners)
	- Provides methods to register and unregister observers dynamically and defines a method to notify observers of changes in its state
- *Observer*
	- Defines an interface with an update method that concrete observers must implement
	- Ensures a common or consistent way for concrete observers to receive updates from the subject
- *ConcreteSubject*
	- Specific implementations of the subject
	- Hold the actual state or data that observers want to track. When this state changes, concrete subjects notify their observers
- *ConcreteObserver*
	- Implements the observer interface. Register with a concrete subject and react when notified of a state change
	- When the subject’s state changes, the concrete observer’s `update()` method is invoked, allowing it to take appropriate actions

```java
import java.util.ArrayList;
import java.util.List;

// Observer Interface
interface Observer {
    void update(String weather);
}

// Subject Interface
interface Subject {
    void addObserver(Observer observer);
    void removeObserver(Observer observer);
    void notifyObservers();
}

// ConcreteSubject Class
class WeatherStation implements Subject {
    private List<Observer> observers = new ArrayList<>();
    private String weather;

    @Override
    public void addObserver(Observer observer) {
        observers.add(observer);
    }

    @Override
    public void removeObserver(Observer observer) {
        observers.remove(observer);
    }

    @Override
    public void notifyObservers() {
        for (Observer observer : observers) {
            observer.update(weather);
        }
    }

    public void setWeather(String newWeather) {
        this.weather = newWeather;
        notifyObservers();
    }
}

// ConcreteObserver Class
class PhoneDisplay implements Observer {
    private String weather;

    @Override
    public void update(String weather) {
        this.weather = weather;
        display();
    }

    private void display() {
        System.out.println("Phone Display: Weather updated - " + weather);
    }
}

// ConcreteObserver Class
class TVDisplay implements Observer {
    private String weather;

    @Override
    public void update(String weather) {
        this.weather = weather;
        display();
    }

    private void display() {
        System.out.println("TV Display: Weather updated - " + weather);
    }
}

// Usage Class
public class WeatherApp {
    public static void main(String[] args) {
        WeatherStation weatherStation = new WeatherStation();

        Observer phoneDisplay = new PhoneDisplay();
        Observer tvDisplay = new TVDisplay();

        weatherStation.addObserver(phoneDisplay);
        weatherStation.addObserver(tvDisplay);

        // Simulating weather change
        weatherStation.setWeather("Sunny");

        // Output:
        // Phone Display: Weather updated - Sunny
        // TV Display: Weather updated - Sunny
    }
}
```