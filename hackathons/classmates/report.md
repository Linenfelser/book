{% import './data.html' as data %}

# Report

Tableau Visulizations: 

https://public.tableau.com/profile/publish/ClassmatesHackathonReport3/Sheet3#!/publish-confirm

https://public.tableau.com/profile/publish/ClassmatesHackathonReport2/Sheet2#!/publish-confirm

https://public.tableau.com/profile/andrew.linenfelser#!/vizhome/ClassmatesHackathonReport/Sheet1



As a class, we brainstormed and came up with a long list of further questions we can ask based
on the "self-introduction" data. Out of these questions, our team chose to tackle on
the following:

# (Percent of students that are CS majors)

{% lodash %}
var bodies = _.pluck(data.comments, 'body')
var cs = _.map(bodies, function( item){return _.last(item.split('Major:'))})
var counter = 0
for(var i=0; i<cs.length; i++){
	if(cs[i].match('Computer Science'))
		counter++
}
var percent = (counter/cs.length) * 100
return percent

{% endlodash %}
{{result}} % of the people are Computer Science people


# (What are the favorite languages?)

{% lodash %}

var bodies = _.pluck(data.comments, 'body')
var cs = _.map(bodies, function( item){return _.last(item.split('Major:'))})
var pythonC = 0
for(var i=0; i<cs.length; i++){
	if(cs[i].match('Python'))
		pythonC++
}return pythonC

var javaC = 0
for(var i=0; i<cs.length; i++){
	if(cs[i].match('Java'))
		javaC++
}//return javaC

var javaScriptC = 0
for(var i=0; i<cs.length; i++){
	if(cs[i].match('Javascript'))
		javaScriptC++
}return javaScriptC

var cC = 0
for(var i=0; i<cs.length; i++){
	if(cs[i].match('C') || cs[i].match('C++') | cs[i].match('C#') )
		cC++
}return cC
console.log(cC)


{% endlodash %}

The results are: {{results}}

# ( How many students submitted before the first class? ) 


{% lodash %}
var created = _.pluck(data.comments, 'created_at')
console.log(created)
var time = _.map(created, function(item){return (item.split('-'))})
var onTime = ["2015-08-24T16:00:00Z"]
var onTimeSplit = _.map(onTime, function(item){return (item.split('-'))})

var counter = 0
for(i=0; i<time.length; i++){
	for(j=0; j<time[i].length; j++){
		if(time[i][j] < onTimeSplit[0][j]){
			//console.log("ON TIME!!!!!")
			counter++
			
		}
	}
}
//console.log(counter)
return counter

{% endlodash %}
{{result}} people submitted before class

# ( How many students updated their comments after class )

{% lodash %}
var created = _.pluck(data.comments, 'updated_at')
var time = _.map(created, function(item){return (item.split('-'))})
var onTime = ["2015-08-24T16:00:00Z"]
var onTimeSplit = _.map(onTime, function(item){return (item.split('-'))})

//console.log("=====================")
//console.log(onTimeSplit)

var counter = 0
for(i=0; i<time.length; i++){
	for(j=0; j<time[i].length; j++){
		if(time[i][j] > onTimeSplit[0][j]){
			//console.log("NOT ON TIME!!!!!")
			counter++
		}
	}
}
return counter
{% endlodash %}

{{result}} people updated after
