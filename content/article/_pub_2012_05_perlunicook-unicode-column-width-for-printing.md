{
   "draft" : null,
   "slug" : "/pub/2012/05/perlunicook-unicode-column-width-for-printing",
   "tags" : [],
   "date" : "2012-05-31T06:00:01-08:00",
   "description" : "â 34: Unicode column-width for printing Perl's printf, sprintf, and format think all codepoints take up 1 print column, but many codepoints take 0 or 2. If you use any of these builtins to align text, you may find that...",
   "thumbnail" : null,
   "categories" : "unicode",
   "title" : "Perl Unicode Cookbook: Unicode Column Width for Printing",
   "image" : null,
   "authors" : [
      "tom-christiansen"
   ]
}





â 34: Unicode column-width for printing {#Unicode-column-width-for-printing}
---------------------------------------

Perl's `printf`, `sprintf`, and `format` think all codepoints take up 1
print column, but many codepoints take 0 or 2. If you use any of these
builtins to align text, you may find that Perl's idea of the width of
any codepoint doesn't match what you think it ought to.

The
[Unicode::GCString](http://search.cpan.org/perldoc?Unicode::GCString)
module's `columns()` method considers the width of each codepoint and
returns the number of columns the string will occupy. Use this to
determine the display width of a Unicode string.

To show that normalization makes no diï¬erence to the number of columns
of a string, we print out both forms:

     # cpan -i Unicode::GCString
     use Unicode::GCString;
     use Unicode::Normalize;

     my @words = qw/crÃ¨me brÃ»lÃ©e/;
     @words    = map { NFC($_), NFD($_) } @words;

     for my $str (@words) {
         my $gcs  = Unicode::GCString->new($str);
         my $cols = $gcs->columns;
         my $pad  = " " x (10 - $cols);
         say str, $pad, " |";
     }

... generates this to show that it pads correctly no matter the
normalization:

     crÃ¨me      |
     creÌme      |
     brÃ»lÃ©e     |
     bruÌleÌe     |

Previous: [â 33: String Length in
Graphemes](/media/_pub_2012_05_perlunicook-unicode-column-width-for-printing/perlunicook-string-length-in-graphemes.html)

Series Index: [The Standard
Preamble](/media/_pub_2012_05_perlunicook-unicode-column-width-for-printing/perlunicook-standard-preamble.html)

Next: [â 35: Unicode
Collation](/media/_pub_2012_05_perlunicook-unicode-column-width-for-printing/perlunicook-unicode-collation.html)

