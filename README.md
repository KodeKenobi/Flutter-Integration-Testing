# screener
- This is a sample Flutter application.
- Uses MVVM pattern
- Tries to encourage the use of boundaries (by using the concept of packages) 

### Getting Started 🎯🎯

- Download the repo
- Make sure you are on the Flutter Stable Channel (1.22.6)

```dart
flutter channel stable
flutter upgrade

```

- Install dependencies, when asked, after downloading the project.
- Run the cmd 
- Run flutter pub get
- Run flutter pub upgrade --major-versions


```dart
- Run flutter run

- You should see the app working at this point..

### Architecture 🏗🏗

- The app follows MVVM approach
- Their is a shared folder, which comprises of all the common entities.
- Common entites like assets, extensions, services etc

- Take a folder, let's say home
- It is broken down into components, models, utils (utilties if any), view and view_models

- Let's discuss each of them

### Components
- They contain the building blocks of UI.
- A UI may comprise of a button, or card, or a list. 
- All these items are created under their respective folders
- Let's say for a list component,

```dart
home/components/list/xyz.component.dart

```

### Model (from MVVM)
- They are usually simple classes
- For instance, let's take home
- It would contain models folder, including all the models needed for home

```dart
home/models/xyz.model.dart

```

### View (from MVVM)
- These are the screens visible to the user on their device.
- For instance, home would have views folder

```dart
home/view/xyz.view.dart

```

- We have 3 views
1. HomeView. Now home has 2 options (Egestas scleri) and (Consectur)
2. On click of Egestas scleri, you see the PellenView
3. On click of Consectur, you see the FringillaView


### Templates
- They are some cases, when a view has a piece of UI, that is somewhat big.
- We extract those bits of UI, into the templates

- Let's say for the home view, we have a template as,

```dart
home/templates/carousel/xyz.template.dart

```

### ViewModel (from MVVM)
- They help in transforming the data into models.
- For instance, home would have view_models folder

```dart
home/view_models/xyz.viewmodel.dart

```

### Utils 
- Any additional helpers or strings are put inside the utils
- For instance, home would have utils folder, containing all the strings needed

```dart
home/utils/strings.dart

```

### Shared
- Their is a folder called shared, which includes all the common entities inside the app

- For instance, all the styles, colors are placed under styles

```dart
shared/styles/xyz.dart

```

- For instance, all the services are placed under the services folder

```dart
shared/services/xyz.service.dart

```

### Data
- Sample data files are put inside the assets
- When needed they are fetched within the app.

### Testing 🧐🧐
- Uses golden tests `https://pub.dev/packages/golden_toolkit`
- Integration tests

```
flutter drive \
--driver=test_driver/integration_test.dart \
--target=integration_test/app_test.dart
```

### Integration Testing Explained
- All the integration tests should be under integration_testing with the name of the file ending in _test. In our case we have one test called app_test.dart 
- Inside our app_test , we first import the package integration test.
- Next we call the ensureInitialized method.
- One of the important points of integration tests is to call the main method of our main app.
- For writing our integration test, we have followed the robot pattern. 

### Robot Testing

- The idea behind robot testing is that the number of screens should be equal to the number of robots. In our app we have 3 screens, Home Robot, Second Robot (where you go after you press the first button when you scroll down) and Third Robot (where you go after you press the second button when you scroll down).
- Inside our app_test file, we create an instance of our robots.
- One of the key points of robot testing is that the test should be readable and self-explanatory on it's own. For example, the HomeRobot says that it should find title, then scroll the page and click the first button. Similarly the SecondScreenRobot also finds the title, scroll the page, scroll the page up and go back.
- Inside the test widgets we initialize the robots by passing it through the widget tester parameters. 

### Home Robot Explained

- We go to home_robot.dart file and we see that it needs a constructor parameter of type widget tester and there are some methods defined like findTitle, scrollThePage, clickFirstButton, clickSecondButton.
- The same goes for our SecondScreenRobot which also takes the WidgetTester parameter and the ThirdScreenRobot.

### Home Screen Tests

- On app_test.dart, the first one is findTitle, we go to the HomeRobot and see the findTitle description  so we call the pumpAndSettle which basically allows the animations to settle in and then next we search for a title and we expect to find one widget and finally we make a call to sleep which comes from dart.io and we make it sleep for 2 seconds.
- Next we call in the scroll. It comprises of a paraeter scrollUp, if this is true , it means we are scrolling towards the up direction., otherwise, we are scrolling in the downwards direction.The fling is responsible for scrolling and here we are passing thre ListFinder and the Offset along with the speed. 
- Our next step is the clickFirstButton. For clickFirstButton we find the button Finder using the key.- We also apply the same behaviour for the second screen, we first find Title and find Title is defined the same as the Home Screen. Next we go to the scroll the page which is exactly the same as the Home Screen.  