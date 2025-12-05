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
    public void diagnostics() {
        class DiagnosticTool {
            public void runTest() {
                System.out.println("Проверка автомобиля " + model + " начата.");
                System.out.println("Диагностика двигателя...");
                System.out.println("Диагностика тормозов...");
                System.out.println("Диагностика электрики...");
                System.out.println("Проверка автомобиля " + model + " завершена.");
            }
        }

        DiagnosticTool diagnosticTool = new DiagnosticTool();
        diagnosticTool.runTest();
    }

    public void performAction(CarAction action) {
        action.execute(this.model);
    }

    public void registerEventListener(CarAction listener) {
        eventListeners.add(listener);
    }

    public void notifyEvent(String event) {
        for (CarAction listener : eventListeners) {
            listener.execute(event);
        }
    }

    public static void main(String[] args) {
        Car myCar = new Car("тип марка");

        myCar.diagnostics();

        myCar.performAction(new CarAction() {
            @Override
            public void execute(String model) {
                System.out.println("Автомобиль " + model + " выполнил экстренное торможение!");
            }
        });

        myCar.performAction(new CarAction() {
            @Override
            public void execute(String model) {
                System.out.println("Автомобиль " + model + " включил автопилот!");
            }
        });

        final int[] count = {0};
        CarAction countingAction = new CarAction() {
            @Override
            public void execute(String model) {
                count[0]++;
                System.out.println("Обработка события №" + count[0] + " для автомобиля " + model);
            }
        };

        countingAction.execute(myCar.model);
        countingAction.execute(myCar.model);
        countingAction.execute(myCar.model);

        myCar.registerEventListener(new CarAction() {
            @Override
            public void execute(String event) {
                System.out.println("[LOGGER] Автомобиль " + myCar.model + ": " + event);
            }
        });

        myCar.registerEventListener(new CarAction() {
            @Override
            public void execute(String event) {
                System.out.println("[WARNING] Внимание! " + event + " в автомобиле " + myCar.model);
            }
        });

        myCar.notifyEvent("низкий уровень топлива");
    }
}

interface CarAction {
    void execute(String model);
}


## Версионирование

В проекте используется [SemVer](https://semver.org/).

## Список релизов

- v1.0.0 — начальная версия проекта.
- v1.1.0 — добавлена класс.
- v1.2.0 — добавлен все остольное.
