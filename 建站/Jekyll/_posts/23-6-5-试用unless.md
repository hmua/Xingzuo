

>- `unless true`{%unless true%}{:.t}{%endunless%}
- `unless false`{%unless false%}{:.t}{%endunless%}
>^
- `unless true and true`{%unless true and true%}{: .t}{%endunless%}
- `unless true and false`{%unless true and false%}{: .t}{%endunless%}
- `unless false and true`{%unless false and true%}{: .t}{%endunless%}
- `unless false and false`{%unless false and false%}{: .t}{%endunless%}
>^
- `unless true or true`{%unless true or true%}{:style='color:green'}{%endunless%}
- `unless true or false`{%unless true or false%}{:style='color:green'}{%endunless%}
- `unless false or true`{%unless false or true%}{:style='color:green'}{%endunless%}
- `unless false or false`{%unless false or false%}{:style='color:green'}{%endunless%}
{: .s}

<style>
.s{color:gray}
.s .t{color:green}
</style>
