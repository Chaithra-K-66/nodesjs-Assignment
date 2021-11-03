Model-View-Controller(MVC)

Controllers are called controllers because of the Model-View-Controller
(MVC) pattern. In the MVC pattern, the Controller is responsible for keeping
the View and the Model in sync. In Angular, this synchronization between the
View and the Model is done by Angular using two-way data-binding. The glue
between the two (View and the Model) is the Angular $scope, which gets
passed to the Controller. The Controller sets up the $scope based on our
application logic. The synchronization of $scope between the view and the
model.

Explanation
Model: Model represents the structure of data, the format and the constraints with which it is stored. 
It maintains the data of the application. Essentially, it is the database part of the application.

View: View is what is presented to the user. Views utilize the Model and present data in a form in which 
the user wants. A user can also be allowed to make changes to the data presented to the user. 
They consist of static and dynamic pages which are rendered or sent to the user when the user requests them.

Controller:Controller controls the requests of the user and then generates appropriate response which is fed to the viewer. 
Typically, the user interacts with the View, which in turn generates the appropriate request, this request will be handled by a
controller. The controller renders the appropriate view with the model data as a response.
So, to sum it up:
	Model is data part.
	View is User Interface part.
	Controller is request-response handler



Demonstration of $scope being the glue between View and Model



Since this model in the Controller is really for the View, it is commonly
called the ViewModel, or vm for short, as we have called it in our example.
Also note that the $scope gets injected into the Controller by Angular. 
We explicitly ask for the $scope by specifying it in the array members. The
relevant segment shown again:

demoApp.controller('MainController', ['$scope', function($scope) {


The initial array members (only '$scope' in this example) drive what
gets passed as the arguments to the final array member, which is our
Controller function. This is one form of dependency injection supported by
Angular. 

Use the $scope from our HTML using directives.The
following HTML’s ng-model keeps the input element in sync with the
vm.name property:
<input type="text" ng-model="vm.name" />


Similarly, call a function on our controller upon a user click using
the ng-click directive:
<button class="btn btn-danger" ng.click="vm.clearName()">Clear Name</button>

Lets get started with the application.
npm init is used here to generate a package.json and app.js file.
As the name suggests, there are three folders, called models, views, controllers which will help in the mvc architecture implementation.
npm is used to install the basic npm packages to get started.

Project Structure Explanation
a)There is aroutes folder, which will serve as controllers.
b)Then there is a models folder, in which we have a user model.
c)A views folder, which have our views with an extension of .handlebars. Be noted that handlebars is a templating engine which 
means that it has the ability to generate the pages by filling in the templating that we create.



