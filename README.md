## #haxtheweb
Copy and paste the following into a bookmarklet to start HAXing the web (Sorta, obviously won't save). Highlight the element you want to modify, click and then HAX will take it over and the UX will tunnel it's way in.

This is what's possible because of custom element style integration. This script below is incredibly small and most of it is because of the initial event binding to actually click on something. All the UX is a single tag on the page and a reference.

Practical uses:
- Demonstrate to someone what HAX UX pattern would look like in their current solution
- Highjack "textarea" tags in order to allow people to excalate them into full on WYSIWYG editor via HAX (again, to show what's possible)
- Cloning parts of websites structure by wrapping it, then injecting, then moving the content into the export area (see developer tools in preferences). Then copying the exported code anywhere else (or downloading it)
```
javascript:(function()%7Bvar%20link%3Ddocument.createElement('link')%3Blink.rel%3D%22import%22%3Bwindow.__appliedHax%20%3D%20false%3Blink.href%3D%22https%3A%2F%2Flrnwebcomponents.github.io%2Fhax-bookmarklet%2Fcomponents%2Fhax-bookmarklet%2Fhax-bookmarklet.html%22%3Bdocument.body.appendChild(link)%3Bvar%20style%3Ddocument.createElement('style')%3Bstyle.innerHTML%20%3D%20'.hax-injected-highlighter%20%7Boutline%3A%202px%20dotted%20%2334e79a%20!important%3Boutline-offset%3A%202px%20!important%3B%7D'%3Bdocument.body.appendChild(style)%3Bdocument.body.addEventListener('click'%2C%20function(e)%7Bif%20(!window.__appliedHax)%20%7Bvar%20org_html%20%3D%20e.target.outerHTML%3Bvar%20new_html%20%3D%20%22%3Chax-bookmarklet%3E%22%20%2B%20org_html%20%2B%20%22%3C%2Fhax-bookmarklet%3E%22%3Be.target.outerHTML%20%3D%20new_html%3Bwindow.__appliedHax%20%3D%20true%3B%7D%7D)%3Bdocument.body.addEventListener('mouseover'%2C%20function(e)%7Bif%20(!window.__appliedHax)%20%7Be.target.classList.add('hax-injected-highlighter')%3B%7D%7D)%3Bdocument.body.addEventListener('mouseout'%2C%20function(e)%7Bif%20(!window.__appliedHax)%20%7Be.target.classList.remove('hax-injected-highlighter')%3B%7D%7D)%7D)()
```

## original source
```
var link=document.createElement('link');
link.rel="import";
window.__appliedHax = false;
link.href="https://lrnwebcomponents.github.io/hax-bookmarklet/components/hax-bookmarklet/hax-bookmarklet.html";
document.body.appendChild(link);
var style=document.createElement('style');
style.innerHTML = '.hax-injected-highlighter {
    outline: 2px dotted #34e79a !important;
    outline-offset: 2px !important;
}';
document.body.appendChild(style);
document.body.addEventListener('click', function(e){
    if (!window.__appliedHax) {
        var org_html = e.target.outerHTML;
        var new_html = "<hax-bookmarklet>" + org_html + "</hax-bookmarklet>";
        e.target.outerHTML = new_html;
        window.__appliedHax = true;
    }
});
document.body.addEventListener('mouseover', function(e){
    if (!window.__appliedHax) {
        e.target.classList.add('hax-injected-highlighter');
    }
});
document.body.addEventListener('mouseout', function(e){
    if (!window.__appliedHax) {
        e.target.classList.remove('hax-injected-highlighter');
    }
});
```