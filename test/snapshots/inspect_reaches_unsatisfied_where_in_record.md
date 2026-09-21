# META
~~~ini
description=Str.inspect on a record reaches a custom to_inspect whose where clause the field's type cannot satisfy (issue 11388)
type=file
~~~
# SOURCE
~~~roc
Nullable(a) := [Null, NotNull(a)].{
	to_inspect : Nullable(a) -> Str where [a.to_inspect : a -> Str]
	to_inspect = |n| match n {
		Null => "Null"
		NotNull(v) => "NotNull(${v.to_inspect()})"
	}
}

show : { id : I64, note : Nullable(Str) } -> Str
show = |row| Str.inspect(row)
~~~
# EXPECTED
MISSING METHOD - inspect_reaches_unsatisfied_where_in_record.md:2:56:2:64
# PROBLEMS
~~~clojure
(reports
	(report
		(severity runtime_error)
		(title "Missing Method")
		(region (start 2 56) (end 2 64))
		(headline
			(reflow "This")
			(reflow " ")
			(annotated code "to_inspect")
			(reflow " ")
			(reflow "method is being called on a value whose type doesn't have that method."))
		(document
			(source-region (file "inspect_reaches_unsatisfied_where_in_record.md") (start 2 56) (end 2 64) (annotation error) (line-text "\tto_inspect : Nullable(a) -> Str where [a.to_inspect : a -> Str]"))
			(line-break)
			(reflow "The value's type, which does not have a method named ")
			(annotated code "to_inspect")
			(reflow ",")
			(reflow " ")
			(reflow "is:")
			(line-break)
			(line-break)
			(annotation-start code-block)
			(indent 1)
			(text "Str")
			(annotation-end)
			(line-break)
			(line-break)
			(annotated emphasis "Hint:")
			(reflow " ")
			(reflow "For this to work, the type would need to have a method named")
			(reflow " ")
			(annotated code "to_inspect")
			(reflow " ")
			(reflow "associated with it in the type's declaration."))))
~~~
# TOKENS
~~~zig
UpperIdent,NoSpaceOpenRound,LowerIdent,CloseRound,OpColonEqual,OpenSquare,UpperIdent,Comma,UpperIdent,NoSpaceOpenRound,LowerIdent,CloseRound,CloseSquare,Dot,OpenCurly,
LowerIdent,OpColon,UpperIdent,NoSpaceOpenRound,LowerIdent,CloseRound,OpArrow,UpperIdent,KwWhere,OpenSquare,LowerIdent,NoSpaceDotLowerIdent,OpColon,LowerIdent,OpArrow,UpperIdent,CloseSquare,
LowerIdent,OpAssign,OpBar,LowerIdent,OpBar,KwMatch,LowerIdent,OpenCurly,
UpperIdent,OpFatArrow,StringStart,StringPart,StringEnd,
UpperIdent,NoSpaceOpenRound,LowerIdent,CloseRound,OpFatArrow,StringStart,StringPart,OpenStringInterpolation,LowerIdent,NoSpaceDotLowerIdent,NoSpaceOpenRound,CloseRound,CloseStringInterpolation,StringPart,StringEnd,
CloseCurly,
CloseCurly,
LowerIdent,OpColon,OpenCurly,LowerIdent,OpColon,UpperIdent,Comma,LowerIdent,OpColon,UpperIdent,NoSpaceOpenRound,UpperIdent,CloseRound,CloseCurly,OpArrow,UpperIdent,
LowerIdent,OpAssign,OpBar,LowerIdent,OpBar,UpperIdent,NoSpaceDotLowerIdent,NoSpaceOpenRound,LowerIdent,CloseRound,
EndOfFile,
~~~
# PARSE
~~~clojure
(file
	(type-mod)
	(statements
		(s-type-decl
			(header (name "Nullable")
				(args
					(ty-var (raw "a"))))
			(ty-tag-union
				(tags
					(ty (name "Null"))
					(ty-apply
						(ty (name "NotNull"))
						(ty-var (raw "a")))))
			(associated
				(s-type-anno (name "to_inspect")
					(ty-fn
						(ty-apply
							(ty (name "Nullable"))
							(ty-var (raw "a")))
						(ty (name "Str")))
					(where
						(method (mod-of "a") (name "to_inspect")
							(ty-fn
								(ty-var (raw "a"))
								(ty (name "Str"))))))
				(s-decl
					(p-ident (raw "to_inspect"))
					(e-lambda
						(args
							(p-ident (raw "n")))
						(e-match
							(e-ident (raw "n"))
							(branches
								(branch
									(p-tag (raw "Null"))
									(e-string
										(e-string-part (raw "Null"))))
								(branch
									(p-tag (raw "NotNull")
										(p-ident (raw "v")))
									(e-string
										(e-string-part (raw "NotNull("))
										(e-method-call (method ".to_inspect")
											(receiver
												(e-ident (raw "v")))
											(args))
										(e-string-part (raw ")"))))))))))
		(s-type-anno (name "show")
			(ty-fn
				(ty-record
					(anno-record-field (name "id")
						(ty (name "I64")))
					(anno-record-field (name "note")
						(ty-apply
							(ty (name "Nullable"))
							(ty (name "Str")))))
				(ty (name "Str"))))
		(s-decl
			(p-ident (raw "show"))
			(e-lambda
				(args
					(p-ident (raw "row")))
				(e-apply
					(e-ident (raw "Str.inspect"))
					(e-ident (raw "row")))))))
~~~
# FORMATTED
~~~roc
NO CHANGE
~~~
# CANONICALIZE
~~~clojure
(can-ir
	(d-let
		(p-assign (ident "inspect_reaches_unsatisfied_where_in_record.Nullable.to_inspect"))
		(e-lambda
			(args
				(p-assign (ident "n")))
			(e-match
				(match
					(cond
						(e-lookup-local
							(p-assign (ident "n"))))
					(branches
						(branch
							(patterns
								(pattern (degenerate false)
									(p-applied-tag)))
							(value
								(e-string
									(e-literal (string "Null")))))
						(branch
							(patterns
								(pattern (degenerate false)
									(p-applied-tag)))
							(value
								(e-block
									(s-let
										(p-assign (ident "#interp_0"))
										(e-runtime-error (tag "erroneous_value_expr")))
									(e-interpolation (constraint-fn-var 326) (dispatcher-var 37)
										(first
											(e-literal (string "NotNull(")))
										(parts
											(e-lookup-local
												(p-assign (ident "#interp_0")))
											(e-literal (string ")")))))))))))
		(annotation
			(ty-fn (effectful false)
				(ty-apply (name "Nullable") (local)
					(ty-rigid-var (name "a")))
				(ty-lookup (name "Str") (builtin)))
			(where
				(method (ty-rigid-var-lookup (ty-rigid-var (name "a"))) (name "to_inspect")
					(ty-fn (effectful false)
						(ty-rigid-var-lookup (ty-rigid-var (name "a")))
						(ty-lookup (name "Str") (builtin)))))))
	(d-let
		(p-assign (ident "show"))
		(e-lambda
			(args
				(p-assign (ident "row")))
			(e-call (constraint-fn-var 349)
				(e-lookup-external
					(builtin))
				(e-lookup-local
					(p-assign (ident "row")))))
		(annotation
			(ty-fn (effectful false)
				(ty-record
					(field (field "id")
						(ty-lookup (name "I64") (builtin)))
					(field (field "note")
						(ty-apply (name "Nullable") (local)
							(ty-lookup (name "Str") (builtin)))))
				(ty-lookup (name "Str") (builtin)))))
	(s-nominal-decl
		(ty-header (name "Nullable")
			(ty-args
				(ty-rigid-var (name "a"))))
		(ty-tag-union
			(ty-tag-name (name "Null"))
			(ty-tag-name (name "NotNull")
				(ty-rigid-var-lookup (ty-rigid-var (name "a")))))))
~~~
# TYPES
~~~clojure
(inferred-types
	(defs
		(patt (type "Nullable(a) -> Str where [a.to_inspect : a -> Str]"))
		(patt (type "{ id: I64, note: Nullable(Str) } -> Str")))
	(type_decls
		(nominal (type "Nullable(a)")
			(ty-header (name "Nullable")
				(ty-args
					(ty-rigid-var (name "a"))))))
	(expressions
		(expr (type "Nullable(a) -> Str where [a.to_inspect : a -> Str]"))
		(expr (type "{ id: I64, note: Nullable(Str) } -> Str"))))
~~~
