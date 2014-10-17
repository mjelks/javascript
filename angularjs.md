AngularJS Intro
- Big Picture
- Views, Directives, and Filters
- Controllers, Scope, and Modules
- Routing
- Services and Factories
	- singleton objects
	- reusable components
	- business rules, calculations, ajax calls, etc.
- Animations
	- css transitions
	- css animations
	- hook them into the directives
	
- Single Page Applications
	- SPAs allow diff. views (screens) to be loaded into a "shell" page
	- Views can be replaced with other views
	- SPAs allow views to be replaced
		- more desktop-like application experience
		- don't reload entire page, just the views
		- maintains a history of views that have been displayed
		
- SPAs rely on many diff. technologies
	- DOM manipulation
	- History Management
	- Routing
	- Ajax
	- Data Binding
	- More
	
- AngularJS takes all the above technologies and combines them together in a single framework
	- data binding
	- MVC
	- routing
	- testing
	- jqLite
	- templates
	- history
	- factories
	- viewmodel
	- controllers
	- views
	- directives
	- services
	
- Getting Started with AngularJS
	- reference the AngularJS script in html page
	- add an 'ng-app' directive
	- gind data using 'directives'
	
- Key Players in AngularJS
	- understand the available parts
	- understand how the parts fit together
	- understand how to organize the parts
	
	- MODULES
		- containers for the components for your application
	- ROUTES
		- path which determines the View that gets loaded
	- UI
		- views
		- directives
		- filters
	- LOGIC/DATA
		- controllers
		- factory
		- service
		
	- $scope binds the UI and LOGIC/DATA together
	
	- what are factories/services?
		- used to make RESTful calls
		- used to share data between controllers
		- used to call custom logic
		- are singletons
		
	- what are controllers?
		- act as the 'brain' for a view
		- retrieve data from a factory/service
		- handle events triggered by the view
		- know how to handle custom logic
		
	- what is $scope?
		- $scope is the "glue" (ViewModel) between a controller and a view
		
	- what are views?
		- views render the user interface
		- contain html and css
	
	- what are routes?
		- each route has a unique path
		- reference a controller and view
		- can include custom params
		
- AngularJS Documentation
	- AngularJS.org -> Develop -> API reference
	
PART 2 : Directives

- Data Binding Overview
	- JS doesn't provide native support for data binding
	- two-way data binding can lead to significant reductions in code
		- properties linked together can update each other
	- control oriented vs data-oriented programming
		- old way == control oriented
			- all controls have ids 
			- example:
				1. code assigns value to a textbox
				2. user modifies data
				3. user clicks a buton
				4. act on the change
		- new way == data-oriented
			- don't even need ids, just wire up properties with proper links
			- example:
				1. Bind a property to a textbox
				2. user modifies data
				3. property value is automatically updated
		


- Directives and Expressions
	- What are Directives?
		- building blocks that teach HTML new tricks
		- key part of AngularJS
	- What can Directive Do?
		- DOM manipulation
		- Data Binding
		- Controllers/Modules
		- View Loading
		- CSS
		- Events
	- Defining Directives
		- most are used at attributes 
			ex: <div ng-hide="isHidden"></div>
		- custom tags
			ex: <ng-view></ng-view>

- Iterating over Data
	- use ng-repeat
	- great for <li> <tr>

- Sorting and Formatting Data
	- use the pipe character
	- key AngularJS filters	
		- currency
		- date
		- filter
		- json
		- limitTo
		- lowercase
		- number
		- orderBy
		- uppercase

PART 3 : Controllers & Scope

- AngularJS Architecture Patterns
	- MVC
	- MVVM
	- Patterns provide prescriptive guidance that can be used to build apps
	- MVC + MVVM = MV*
		- combination of multiple patterns
		- request -> Controller (brain for a given view) 
					<-> communicate with the model 
					-> put data into the $scope 
					-> view accesses props via $scope
		  response  <-

- The Role of Controllers
	- act as the brain for your view
		- define props. and methods
		- handle show/hide controls and data in a view
		- handle events triggered by a view
		- know how to retrieve data
		- interacts with the view via the $scope 
	- the role of $scope
		- keyword in AngularJS 
		- automatically "injected" into a controller
		- acts as the ViewModel
		- views bind to scope props. and functions
	- example
		// $scope (a data-container) automatically injected by AngularJS
		function SimpleController($scope) {
			$scope.customers = [
				{ name: "danny", city: 'Tucson'}
			];
		}
	
- The ng-controller directive
	- Tying a View and Controller together
		- use of the ng-controller directive
		- "controller as" method

- The Role of Modules
	- What is a module?
		containers for : (pulls these things out of 'global' scope)
		- routes
		- controllers
		- factories/services
		- directives
		- filters
	- Syntax
		<html ng-app="moduleName">
	- Creation
		var demoApp = angular.module('demoApp', [])
			- array bracket is for dependencies
		example: helper modules can be "injected" into your module
			var demoApp = angular.module('demoApp',['helperModule','thirdPartyModule'])

- Adding a Controller to a Module
	option 1:
	// global variable demoApp throughout code (might be an issue)
	var demoApp = angular.module('demoApp', []);
	
	demoApp.controller('SimpleController', function($scope) {
		// code here
	}
	
	option 2: reference the demoApp global
	var demoApp = angular.module('demoApp', []);
	angular.module('demoApp').controller('SimpleController, function($scope) {
		// code here
	}

	option 3: wrap in anonymous function
	var demoApp = angular.module('demoApp', []);
	
	(function() {
		var SimpleController = function ($scope) {
			$scope.customers...
		};
		
		angular.module('demoApp').controller('SimpleController'), SimpleController);
	} ());
	

	dealing with minification
	angular.module('demoApp')
		.controller('SimpleController', ['$scope', function ($scope) {
		}]);
		
	OR
	
	SimpleController.$inject = ['$scope']
	
PART 4: Routing

	- Routing Overview
		- marry view with controller
		- important in SPAs in general
		- history / navigation management
		- relies on ngRoute module (separate script)
		- routes configured using $routeProvider (AngularJS built-in)
		- routes configured by :
			angular.module.config()
			$routeProvider injected dynamically
	
	- Referencing the ngRoute Module
		- Add a <script> tag that loads angular-route.js script
			- right after loading angular.js
		- reference ngRoute in your module
			- var demoApp = angular.module('demoApp', ['ngRoute'])
	
	- Configuring Routes
		- use routeProvider object to associate route with view/controller
	
	- Using the ng-view Directive
	
	- Summary
		- built-in support for routing
		- routes associate view w/ controller
		- NEED TO reference the ngRoute module (not built-in to core)
		- $routeProvider injected into angular.module.config()
		- route parameters are key (similar to rails design)
		
PART 5: Factories and Services
	- Overview
		- shared code across controllers
		- built directly into AngularJS Framework
		- injected into a Controller
		
	- Factory and Service Overview
		- AngularJS includes several built-in factories/services
		- singletons
			- Ajax calls
			- business rules
			- calculations
			- data sharing between controllers
		- can create your own using the Module approach
		- built-ins: (services)
			- $http
			- $timeout
			- $window
			- $location
			- $q (async processes)
			- $rootScope
			- $interval (repeating type timer)
			- $filter
			- $log
	
	- Creating a Factory
		- define reusable tasks
		- share code between controllers
		- create and return a custom object
		- created using the module.factory() function
		- can be injected into other components
		- can have dependencies
	
	- Creating a Service
		- similar to a factory as far as functionality
		- represents the returned object as opposed to a custom object like in a factory
		- created using the module.service() function
		- can be injected into other components
		- factory == custom object
		- service == function IS the object
	
	- Defining Application Values
		- value
			- a value can be created by module.value(key, value)
			- can't be injected into the config
		- constants
			- a constant can be created by using module.constant(key, value)
			- CAN be injected into the config (earlier in the lifecycle)
	
	- Making AJAX Calls from a Factory/Service
		- $http
			- provided out of the box
			- provides Ajax functionality
			- uses XmlHttpRequest object
			- async
			- supports multiple HTTP verbs
		$http makes async call
			- relies on on $q service's deferred / promise API
			- access data by calling then() or success()/error()
			
PART 6: UI and Animation
	- Enhancing the UI with Bootstrap
	
	- Animation Overview
		- Animation hooks for built-in and custom directives
		- animations triggered by diff. scenarios
		- include ngAnimate module
		- COMMON Directives
			- ngClass
			- ngHide/ngShow
			- ngInclude
			- ngRepeat
			- ngSwitch
			- ngView
		- Custom Directives
			- $animate service
		- good resource:
			http://augus.github.io/ngAnimate
			http://www.yearofmoo.com
			http://daneden.me/animate/
			
	- The ngAnimate Module
	
	- Defining Animations in CSS
		- options:
			- using css3 transitions
			- using css3 animations
			- javascript animations (compat. with older browsers)
			
		- CSS Transitions
			transition: 0.5s linear all;
		
		- CSS Animations
			- keyframes
	
	- Referencing Animation Classes
	
	- Summary
		- AngularJS provides built-in suport for animations using CSS or JavaScript
		- Reference the ngAnimate script and module
		- Several directives such as ng-view and ng-repeat support animations
		- Use CSS transitions or animations to create custom animations
	
	
			
			
		
		
	
	
