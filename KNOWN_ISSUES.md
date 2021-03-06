Known Issues
============

This document describes known issues in Zubr. 

mod.main
----------------------------------

for now, the pipeline can only call mod.main imports, should be changes
so that script files can call arbitrary functions 

lisp defun
------------------------------------
Lisp defun has issues when the comment spans multiple lines

gzip OverflowError
-------------------------------------

ZubrClass automatically gzips large objects (e.g., models), and
crashes when the models get large, resulting in an
OverflowError. Apparently this is a underlying problem in python 2.7 

http://stackoverflow.com/questions/33562394/gzip-raised-overflowerror-size-does-not-fit-in-an-unsigned-int

I've tried to replace gzip with bz2, which is very slow. Current I'm
using lz4 compression for large models (dump_large is the name of the
ZubrClass method used). 

concurrent graph decoder
---------------------------------------
The concurrent graph decoders sometimes ranks slightly different than
the non-concurrent models. Perhaps there is a slight difference in the
models used when copied, or when uses a trained model from file. The
difference so far doesn't seem significant, but might make a
difference in the evaluation if comparing output generated by the
different decoders.

