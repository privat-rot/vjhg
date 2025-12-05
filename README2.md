# devsecops

import java.util.*;

public class Car {
    private String model;
    private List<CarAction> eventListeners = new ArrayList<>();

    public Car(String model) {
        this.model = model;
    }
}
