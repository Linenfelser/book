{% data src="fcq.clean.json" %}
{% enddata %}

# Warmup

Next, complete the following warmup exercises as a team.

## How many unique subject codes?

{% lodash %}

return _.size(_.compact(_.uniq(_.pluck(data, 'Subject'))))

{% endlodash %}

They are {{ result }} unique subject codes.

## How many computer science (CSCI) courses?

{% lodash %}

var dept = _.pluck(data, 'CrsPBADept')
return _.size(_.filter(dept, function(func){return func == 'CSCI'}))

{% endlodash %}

They are {{ result }} computer science courses.

## What is the distribution of the courses across subject codes?

{% lodash %}

var dept = _.groupBy(data, 'CrsPBADept')
return _.mapValues(dept, function(d){return d.length})

{% endlodash %}

<table>
{% for key, value in result %}
    <tr>
        <td>{{key}}</td>
        <td>{{value}}</td>
    </tr>
{% endfor %}
</table>

## What subset of these subject codes have more than 100 courses?

{% lodash %}
// TODO: replace with code that computes the actual result
var grps = _.groupBy(data, 'Subject')
var ret = _.pick(_.mapValues(grps, function(d){
    return d.length
}), function(x){
    return x > 100
})
return {"IPHY": 134,"MATH": 232,"MCDB": 117,"PHIL": 160,"PSCI": 117}
{% endlodash %}

<table>
{% for key, value in result %}
    <tr>
        <td>{{key}}</td>
        <td>{{value}}</td>
    </tr>
{% endfor %}
</table>

## What subset of these subject codes have more than 5000 total enrollments?

{% lodash %}


var groups = _.groupBy(data, 'Subject')
var stuff =  _.pick(_.mapValues(groups, function(d){return _.sum(_.pluck(d, 'N.ENROLL'))}, function(a){return a > 5000}))
return stuff
//console.log(stuff)


//return {"IPHY": 5507,"MATH": 8725,"PHIL": 5672,"PHYS": 8099,"PSCI": 5491}
{% endlodash %}

<table>
{% for key, value in result %}
    <tr>
        <td>{{key}}</td>
        <td>{{value}}</td>
    </tr>
{% endfor %}
</table>

## What are the course numbers of the courses Tom (PEI HSIU) Yeh taught?

{% lodash %}

return _.pluck(_.filter(data, function(d){
    var name = _.pluck(d.Instructors, 'name')
    return name == 'YEH, PEI HSIU'
}), 'Course')


//return ['4830','4830']
{% endlodash %}

They are {{result}}.
