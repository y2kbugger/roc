# META
~~~ini
description=Str.inspect on a record reaches a custom to_inspect that does not return Str
type=file
~~~
# SOURCE
~~~roc
Bad := [B].{
	to_inspect : Bad -> U64
	to_inspect = |_| 1
}

show : { x : Bad } -> Str
show = |r| Str.inspect(r)
~~~
# EXPECTED
TYPE MISMATCH - inspect_reaches_wrong_sig_in_record.md:6:14:6:17
# PROBLEMS
~~~clojure
(reports
	(report
		(severity runtime_error)
		(title "Type Mismatch")
		(region (start 6 14) (end 6 17))
		(headline
			(reflow "The")
			(reflow " ")
			(annotated code "to_inspect")
			(reflow " ")
			(reflow "method on")
			(reflow " ")
			(annotated code "Bad")
			(reflow " ")
			(reflow "has an incompatible type."))
		(document
			(source-region (file "inspect_reaches_wrong_sig_in_record.md") (start 6 14) (end 6 17) (annotation error) (line-text "show : { x : Bad } -> Str"))
			(line-break)
			(reflow "The method")
			(reflow " ")
			(annotated code "to_inspect")
			(reflow " ")
			(reflow "has the type:")
			(line-break)
			(line-break)
			(annotation-start code-block)
			(indent 1)
			(text "Bad -> U64")
			(annotation-end)
			(line-break)
			(line-break)
			(reflow "But I need it to have the type:")
			(line-break)
			(line-break)
			(annotation-start code-block)
			(indent 1)
			(text "Bad -> Str")
			(annotation-end))))
~~~
# TOKENS
~~~zig
UpperIdent,OpColonEqual,OpenSquare,UpperIdent,CloseSquare,Dot,OpenCurly,
LowerIdent,OpColon,UpperIdent,OpArrow,UpperIdent,
LowerIdent,OpAssign,OpBar,Underscore,OpBar,Int,
CloseCurly,
LowerIdent,OpColon,OpenCurly,LowerIdent,OpColon,UpperIdent,CloseCurly,OpArrow,UpperIdent,
LowerIdent,OpAssign,OpBar,LowerIdent,OpBar,UpperIdent,NoSpaceDotLowerIdent,NoSpaceOpenRound,LowerIdent,CloseRound,
EndOfFile,
~~~
# PARSE
~~~clojure
(file
	(type-mod)
	(statements
		(s-type-decl
			(header (name "Bad")
				(args))
			(ty-tag-union
				(tags
					(ty (name "B"))))
			(associated
				(s-type-anno (name "to_inspect")
					(ty-fn
						(ty (name "Bad"))
						(ty (name "U64"))))
				(s-decl
					(p-ident (raw "to_inspect"))
					(e-lambda
						(args
							(p-underscore))
						(e-int (raw "1"))))))
		(s-type-anno (name "show")
			(ty-fn
				(ty-record
					(anno-record-field (name "x")
						(ty (name "Bad"))))
				(ty (name "Str"))))
		(s-decl
			(p-ident (raw "show"))
			(e-lambda
				(args
					(p-ident (raw "r")))
				(e-apply
					(e-ident (raw "Str.inspect"))
					(e-ident (raw "r")))))))
~~~
# FORMATTED
~~~roc
NO CHANGE
~~~
# CANONICALIZE
~~~clojure
(can-ir
	(d-let
		(p-assign (ident "inspect_reaches_wrong_sig_in_record.Bad.to_inspect"))
		(e-lambda
			(args
				(p-underscore))
			(e-num (value "1")))
		(annotation
			(ty-fn (effectful false)
				(ty-lookup (name "Bad") (local))
				(ty-lookup (name "U64") (builtin)))))
	(d-let
		(p-assign (ident "show"))
		(e-lambda
			(args
				(p-assign (ident "r")))
			(e-runtime-error (tag "erroneous_value_expr")))
		(annotation
			(ty-fn (effectful false)
				(ty-record
					(field (field "x")
						(ty-lookup (name "Bad") (local))))
				(ty-lookup (name "Str") (builtin)))))
	(s-nominal-decl
		(ty-header (name "Bad"))
		(ty-tag-union
			(ty-tag-name (name "B")))))
~~~
# TYPES
~~~clojure
(inferred-types
	(defs
		(patt (type "Error"))
		(patt (type "{ x: Bad } -> Error")))
	(type_decls
		(nominal (type "Bad")
			(ty-header (name "Bad"))))
	(expressions
		(expr (type "Bad -> U64"))
		(expr (type "{ x: Bad } -> Error"))))
~~~
