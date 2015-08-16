---
date: "2013-08-23"
title: Automatically setting height of textarea to height of its contents on page load
type: post
---

jQuery makes everything so ridiculously simple. To make sure a textarea is automatically resized so it fits its content one could calculate the amount of rows of text and the approximate height of the font and set the height of the textarea to the product of that. Or you could set the height to the scroll size with jQuery and JavaScript.

    <script>
        $(function() {
             $('textarea').height($('textarea').prop('scrollHeight'));
        });
    </script>

Admittedly, it's not a complete solution if you need it on a page with more than one textarea though. Then it goes from a one-liner to a three-liner.

    <script>
        $(function() {
            $('textarea').each(function() {
                $(this).height($(this).prop('scrollHeight'));
            });
        });
    </script>
