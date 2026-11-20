## Ex.No:5 Develop a simple calculator using android studio.
## AIM:

To develop a program to develop a simple calculator in Android Studio.

## EQUIPMENTS REQUIRED:
Android Studio(Min.required Artic Fox)

## ALGORITHM:
Step 1: Open Android Stdio and then click on File -> New -> New project.

Step 2: Then type the Application name as calculator and click Next.

Step 3: Then select the Minimum SDK as shown below and click Next.

Step 4: Then select the Empty Activity and click Next. Finally click Finish.

Step 5: Design layout using UI components in activity_main.xml.

Step 6: Display the calculator operation in MainActivity file.

Step 7: Save and run the application.

## PROGRAM:
/*
Program to print the text “calculator operation”.
Developed by: TAMILSELVI P
Registeration Number : 212225040460
*/

## ACTIVITY_MAIN.XML
```
<?xml version="1.0" encoding="utf-8"?>
<LinearLayout xmlns:android="http://schemas.android.com/apk/res/android"
    android:layout_width="match_parent"
    android:layout_height="match_parent"
    android:orientation="vertical"
    android:background="#101820"
    android:padding="16dp">

    <!-- Display Area -->
    <LinearLayout
        android:layout_width="match_parent"
        android:layout_height="0dp"
        android:layout_weight="1"
        android:gravity="bottom"
        android:orientation="vertical"
        android:padding="16dp">

        <!-- Expression -->
        <TextView
            android:id="@+id/expression"
            android:layout_width="match_parent"
            android:layout_height="wrap_content"
            android:gravity="end"
            android:text=""
            android:textColor="#8FA3B8"
            android:textSize="22sp"
            android:maxLines="1"/>

        <!-- Result -->
        <TextView
            android:id="@+id/display"
            android:layout_width="match_parent"
            android:layout_height="wrap_content"
            android:gravity="end"
            android:text="0"
            android:textColor="#FFFFFF"
            android:textSize="48sp"
            android:maxLines="1"
            android:ellipsize="start"/>

    </LinearLayout>

    <!-- Row 1 -->
    <LinearLayout
        android:layout_width="match_parent"
        android:layout_height="wrap_content"
        android:orientation="horizontal">

        <Button
            android:id="@+id/btnClear"
            android:text="AC"
            style="@style/CalculatorFunctionButton"/>

        <Button
            android:id="@+id/btnSign"
            android:text="+/-"
            style="@style/CalculatorFunctionButton"/>

        <Button
            android:id="@+id/btnPercent"
            android:text="%"
            style="@style/CalculatorFunctionButton"/>

        <Button
            android:id="@+id/btnDivide"
            android:text="÷"
            style="@style/CalculatorOperatorButton"/>

    </LinearLayout>

    <!-- Row 2 -->
    <LinearLayout
        android:layout_width="match_parent"
        android:layout_height="wrap_content"
        android:orientation="horizontal">

        <Button
            android:id="@+id/btn7"
            android:text="7"
            style="@style/CalculatorNumberButton"/>

        <Button
            android:id="@+id/btn8"
            android:text="8"
            style="@style/CalculatorNumberButton"/>

        <Button
            android:id="@+id/btn9"
            android:text="9"
            style="@style/CalculatorNumberButton"/>

        <Button
            android:id="@+id/btnMultiply"
            android:text="×"
            style="@style/CalculatorOperatorButton"/>

    </LinearLayout>

    <!-- Row 3 -->
    <LinearLayout
        android:layout_width="match_parent"
        android:layout_height="wrap_content"
        android:orientation="horizontal">

        <Button
            android:id="@+id/btn4"
            android:text="4"
            style="@style/CalculatorNumberButton"/>

        <Button
            android:id="@+id/btn5"
            android:text="5"
            style="@style/CalculatorNumberButton"/>

        <Button
            android:id="@+id/btn6"
            android:text="6"
            style="@style/CalculatorNumberButton"/>

        <Button
            android:id="@+id/btnSubtract"
            android:text="−"
            style="@style/CalculatorOperatorButton"/>

    </LinearLayout>

    <!-- Row 4 -->
    <LinearLayout
        android:layout_width="match_parent"
        android:layout_height="wrap_content"
        android:orientation="horizontal">

        <Button
            android:id="@+id/btn1"
            android:text="1"
            style="@style/CalculatorNumberButton"/>

        <Button
            android:id="@+id/btn2"
            android:text="2"
            style="@style/CalculatorNumberButton"/>

        <Button
            android:id="@+id/btn3"
            android:text="3"
            style="@style/CalculatorNumberButton"/>

        <Button
            android:id="@+id/btnAdd"
            android:text="+"
            style="@style/CalculatorOperatorButton"/>

    </LinearLayout>

    <!-- Row 5 -->
    <LinearLayout
        android:layout_width="match_parent"
        android:layout_height="wrap_content"
        android:orientation="horizontal">

        <Button
            android:id="@+id/btn0"
            android:text="0"
            style="@style/CalculatorNumberButton"/>

        <Button
            android:id="@+id/btnDot"
            android:text="."
            style="@style/CalculatorNumberButton"/>

        <Button
            android:id="@+id/btnEqual"
            android:text="="
            style="@style/CalculatorOperatorButton"/>

    </LinearLayout>

</LinearLayout>

```

## MAINACTIVITY.JAVA
```
package com.example.calculator;

import android.os.Bundle;
import android.widget.Button;
import android.widget.TextView;

import androidx.appcompat.app.AppCompatActivity;

public class MainActivity extends AppCompatActivity {

    TextView display, expression;

    double firstNumber = 0;
    String operator = "";
    String currentInput = "";
    boolean newNumber = true;

    @Override
    protected void onCreate(Bundle savedInstanceState) {
        super.onCreate(savedInstanceState);
        setContentView(R.layout.activity_main);

        display = findViewById(R.id.display);
        expression = findViewById(R.id.expression);

        int[] numberIds = {
                R.id.btn0, R.id.btn1, R.id.btn2, R.id.btn3,
                R.id.btn4, R.id.btn5, R.id.btn6, R.id.btn7,
                R.id.btn8, R.id.btn9, R.id.btnDot
        };

        for (int id : numberIds) {

            Button button = findViewById(id);

            button.setOnClickListener(v -> {

                String value = button.getText().toString();

                if (newNumber) {
                    currentInput = "";
                    newNumber = false;
                }

                if (value.equals(".")) {

                    if (!currentInput.contains(".")) {

                        if (currentInput.isEmpty()) {
                            currentInput = "0";
                        }

                        currentInput += ".";
                    }

                } else {

                    currentInput += value;
                }

                updateDisplay();
            });
        }

        findViewById(R.id.btnAdd).setOnClickListener(v -> setOperator("+"));

        findViewById(R.id.btnSubtract).setOnClickListener(v -> setOperator("-"));

        findViewById(R.id.btnMultiply).setOnClickListener(v -> setOperator("×"));

        findViewById(R.id.btnDivide).setOnClickListener(v -> setOperator("÷"));

        findViewById(R.id.btnEqual).setOnClickListener(v -> calculate());

        findViewById(R.id.btnClear).setOnClickListener(v -> clear());

        findViewById(R.id.btnSign).setOnClickListener(v -> changeSign());

        findViewById(R.id.btnPercent).setOnClickListener(v -> percentage());
    }

    void setOperator(String op) {

        if (currentInput.isEmpty()) {

            if (!operator.isEmpty()) {
                operator = op;
                updateDisplay();
            }

            return;
        }

        if (!operator.isEmpty() && !newNumber) {
            calculate();
        }

        try {

            firstNumber = Double.parseDouble(currentInput);
            operator = op;
            currentInput = "";
            newNumber = false;

            updateDisplay();

        } catch (Exception e) {

            display.setText("Error");
        }
    }

    void updateDisplay() {

        if (operator.isEmpty()) {

            display.setText(currentInput.isEmpty() ? "0" : currentInput);

        } else {

            display.setText(currentInput.isEmpty()
                    ? formatResult(firstNumber)
                    : currentInput);
        }
    }

    void calculate() {

        if (operator.isEmpty() || currentInput.isEmpty()) {
            return;
        }

        try {

            double secondNumber = Double.parseDouble(currentInput);

            String oldExpression = formatResult(firstNumber)
                    + " " + operator + " " + currentInput;

            double result = 0;

            switch (operator) {

                case "+":
                    result = firstNumber + secondNumber;
                    break;

                case "-":
                    result = firstNumber - secondNumber;
                    break;

                case "×":
                    result = firstNumber * secondNumber;
                    break;

                case "÷":

                    if (secondNumber == 0) {

                        expression.setText("");
                        display.setText("Error");

                        clear();
                        return;
                    }

                    result = firstNumber / secondNumber;
                    break;
            }

            expression.setText(oldExpression);

            currentInput = formatResult(result);

            display.setText(currentInput);

            firstNumber = result;
            operator = "";
            newNumber = true;

        } catch (Exception e) {

            display.setText("Error");
            clear();
        }
    }

    String formatResult(double number) {

        if (number == (long) number) {

            return String.valueOf((long) number);
        }

        return String.valueOf(number);
    }

    void clear() {

        firstNumber = 0;
        operator = "";
        currentInput = "";
        newNumber = true;

        display.setText("0");
        expression.setText("");
    }

    void changeSign() {

        if (currentInput.isEmpty()) {
            return;
        }

        try {

            double number = Double.parseDouble(currentInput);

            number = -number;

            currentInput = formatResult(number);

            newNumber = false;

            updateDisplay();

        } catch (Exception e) {

            display.setText("Error");
        }
    }

    void percentage() {

        if (currentInput.isEmpty()) {
            return;
        }

        try {

            double number = Double.parseDouble(currentInput);

            number = number / 100;

            currentInput = formatResult(number);

            newNumber = false;

            updateDisplay();

        } catch (Exception e) {

            display.setText("Error");
        }
    }
}

```

## STYLES.XML
```
<?xml version="1.0" encoding="utf-8"?>
<resources>

    <style name="CalculatorNumberButton">
        <item name="android:layout_width">0dp</item>
        <item name="android:layout_height">58dp</item>
        <item name="android:layout_weight">1</item>
        <item name="android:layout_margin">4dp</item>
        <item name="android:backgroundTint">#263746</item>
        <item name="android:textColor">#FFFFFF</item>
        <item name="android:textSize">22sp</item>
        <item name="android:textStyle">bold</item>
        <item name="android:minHeight">0dp</item>
        <item name="android:minWidth">0dp</item>
        <item name="android:stateListAnimator">@null</item>
    </style>

    <style name="CalculatorFunctionButton" parent="CalculatorNumberButton">
        <item name="android:backgroundTint">#B8D8D8</item>
        <item name="android:textColor">#152A38</item>
    </style>

    <style name="CalculatorOperatorButton" parent="CalculatorNumberButton">
        <item name="android:backgroundTint">#4DB6AC</item>
        <item name="android:textColor">#FFFFFF</item>
    </style>

</resources>

```

## OUTPUT:

<img width="1920" height="1080" alt="Screenshot (284)" src="https://github.com/user-attachments/assets/22cd5d31-b761-46fe-9012-e517f2fcd3cd" />

<img width="1920" height="1080" alt="Screenshot (285)" src="https://github.com/user-attachments/assets/95f4bca1-6ea6-473e-a196-5262c0e4cbb1" />

<img width="1920" height="1080" alt="Screenshot (286)" src="https://github.com/user-attachments/assets/856f4ff2-61ea-4750-9698-2de32e27f319" />


<img width="1920" height="1080" alt="Screenshot (288)" src="https://github.com/user-attachments/assets/04f9fcaa-7689-4695-b836-c6ee2e7f53dc" />


## RESULT:


  Thus the program was executed successfully.
