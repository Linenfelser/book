# Analysis

{% import './data.html' as data %}

After completing the warmup exercises, your task is to do four more slightly
more challenges analyses.

## How many students like sushi as their favorite food?

{% lodash %}
var bodies = _.pluck(data.comments, 'body')
var food = _.map(bodies, function( item){return _.last(item.split('Food:'))})
var counter = 0
for(var i=0; i<food.length; i++){
	if((food[i].match('Sushi')) || food[i].match('sushi')) 
		counter++
}
return counter

{% endlodash %}

The answer is {{result}}.

## Who are the students liking Python the most?

{% lodash %}
var python = _.filter(data.comments, function(py){ return _.includes(py.body, "Python"); })
var bodiesPython = _.pluck(python, 'body')

var myArray = []
for(i=0; i<bodiesPython.length; i++){
	var name = _.first(bodiesPython[i].split('\r\n'))
	//console.log(name)
	myArray.push(name)
}
return myArray

{% endlodash %}

Their names are {{result}}.

## Are there more Javascript lovers or Java lovers?

{% lodash %}
var bodies = _.pluck(data.comments, 'body')
var whichOne = _.map(bodies, function(item){return _.last(item.split('Language:'))})
var counterJava = 0
var counterScript = 0
for(var i=0; i<whichOne.length; i++){
	if(whichOne[i].match('Java\r') || whichOne[i].match('java\r') || whichOne[i].match('JAVA\r')) 
		counterJava++
	if(whichOne[i].match('Javascript') || whichOne[i].match('javascript'))
		counterScript++	
}
if(counterJava > counterScript)
	return 'Java'

if(counterJava < counterScript)
	return 'Javascript'
else return 'The same'

{% endlodash %}

The answer is {{result}}.

## Who likes the same food as `kjblakemore`?

{% lodash %}
var kjb = _.filter(_.pluck(data.comments, 'body'), function(text){return _.includes(text, 'Vegan')})
//console.log(kjb)
var names = _.map(kjb, function(n){return _.last(n.split('Name:'))})
var myArray = []
for(i=0; i<names.length; i++){
	var name = _.first(names[i].split('\r\n'))
	myArray.push(name)
}
return myArray



{% endlodash %}
The people who like the same food as kjblakemore are: {{result}}.
