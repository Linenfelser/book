{% data src="fcq.clean.json" %}
{% enddata %}

# Report

As a class, we brainstormed and came up with a long list of further questions we
can ask based on the FCQ data. Out of these questions, our team chose to tackle on
the following questions. Each member on our team is reponsible for one question.

# (Question 1) by (Name)

{% lodash %}
return "[answer]"
{% endlodash %}


# (Question 2) by (Name)

{% lodash %}
return "[answer]"
{% endlodash %}


# (Question 3) by (Name)

{% lodash %}
return "[answer]"
{% endlodash %}

# (Question 4) by (Name)

{% lodash %}
return "[answer]"
{% endlodash %}

# (Which course level has the lowest retention?) by (Andrew)

{% lodash %}

var level = _.groupBy(data, 'Level')
var ret = _.pairs(_.mapValues(level, function(d){return (_.sum(_.pluck(d, 'PCT.WDRAW'))/d.length)*100}))
return _.sortBy(ret, function(d){return d[1]})


{% endlodash %}

<table>
{% for key, value in result %}
    <tr>
        <td>{{key}}</td>
        <td>{{value}}</td>
    </tr>
{% endfor %}
</table>













