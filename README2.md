# devsecops

import java.util.*;

public class Car {
    private String model;
    private List<CarAction> eventListeners = new ArrayList<>();

    public Car(String model) {
        this.model = model;
    }

    public class CarManual {
        private final String language;

        public CarManual(String language) {
            this.language = language;
        }

        public void printInstructions() {
            System.out.println("Инструкция на языке " + language + ": ****");
        }
    }
}
