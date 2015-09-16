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

var language_string = ""
for (i = 0; i < _.size(data.comments); i++) {
    var text = data.comments[i].body
    var languages

    function splitString(stringToSplit, separator) {
        var arrayOfStrings = stringToSplit.split(separator)
        var language_line = arrayOfStrings[2]
        var line = language_line.split(':')
        var favorite_language = line[1]
        var splitline = favorite_language.split(" ")

        if (favorite_language != "") {
            return (splitline[1])
        }
        else {
            return 'false'
        }
    }

    languages = splitString(text, '\r\n')
    if (languages == "JAVA") {languages = "Java"}
    language_string += (_.capitalize(languages) + ',')
}

var array = language_string.split(',')
var saved_array = language_string.split(',')
var new_array = array
var key = array[0].split()
var found_keys = key + ','

while (new_array.length > 1) {
    new_array = _.difference(array, key)
    array = new_array
    key = new_array[0].split()
    found_keys += (key + ',')
}

var sort_keys = found_keys.split(",")
var answer = ""

for (var i = 0; i < sort_keys.length; i++) {
    if (sort_keys[i] != "") {
    var count = 0
        for (var j = 0; j < saved_array.length; j++) {
            if(saved_array[j] == sort_keys[i]) { count++ }
        }
        answer += (sort_keys[i] + ':' + count + ' ')
    }
}

return answer


console.log(answer)



{% endlodash %}

The results are: {{result}}

# ( How many students submitted before the first class? ) 


{% lodash %}
var created = _.pluck(data.comments, 'created_at')
console.log(created)
var time = _.map(created, function(item){return (item.split('-'))})
var onTime = ["2015-08-24T22:00:00Z"]
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
var onTime = ["2015-08-24T22:00:00Z"]
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
