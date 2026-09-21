# META
~~~ini
description=Str.inspect reaches an unsatisfiable custom to_inspect through a list, a tuple, a tag payload, a Box and a transparent nominal, but not through an opaque one (issue 11388)
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

Wrapper := { note : Nullable(Str) }

Hidden :: { note : Nullable(Str) }

in_list : List(Nullable(Str)) -> Str
in_list = |v| Str.inspect(v)

in_tuple : (I64, Nullable(Str)) -> Str
in_tuple = |v| Str.inspect(v)

in_tag : [Some(Nullable(Str)), None] -> Str
in_tag = |v| Str.inspect(v)

in_box : Box(Nullable(Str)) -> Str
in_box = |v| Str.inspect(v)

in_nominal : Wrapper -> Str
in_nominal = |v| Str.inspect(v)

in_opaque : Hidden -> Str
in_opaque = |v| Str.inspect(v)
~~~
# EXPECTED
MISSING METHOD - inspect_reaches_unsatisfied_where_through_shapes.md:2:56:2:64
MISSING METHOD - inspect_reaches_unsatisfied_where_through_shapes.md:2:56:2:64
MISSING METHOD - inspect_reaches_unsatisfied_where_through_shapes.md:2:56:2:64
MISSING METHOD - inspect_reaches_unsatisfied_where_through_shapes.md:2:56:2:64
MISSING METHOD - inspect_reaches_unsatisfied_where_through_shapes.md:2:56:2:64
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
			(source-region (file "inspect_reaches_unsatisfied_where_through_shapes.md") (start 2 56) (end 2 64) (annotation error) (line-text "\tto_inspect : Nullable(a) -> Str where [a.to_inspect : a -> Str]"))
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
			(reflow "associated with it in the type's declaration.")))
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
			(source-region (file "inspect_reaches_unsatisfied_where_through_shapes.md") (start 2 56) (end 2 64) (annotation error) (line-text "\tto_inspect : Nullable(a) -> Str where [a.to_inspect : a -> Str]"))
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
			(reflow "associated with it in the type's declaration.")))
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
			(source-region (file "inspect_reaches_unsatisfied_where_through_shapes.md") (start 2 56) (end 2 64) (annotation error) (line-text "\tto_inspect : Nullable(a) -> Str where [a.to_inspect : a -> Str]"))
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
			(reflow "associated with it in the type's declaration.")))
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
			(source-region (file "inspect_reaches_unsatisfied_where_through_shapes.md") (start 2 56) (end 2 64) (annotation error) (line-text "\tto_inspect : Nullable(a) -> Str where [a.to_inspect : a -> Str]"))
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
			(reflow "associated with it in the type's declaration.")))
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
			(source-region (file "inspect_reaches_unsatisfied_where_through_shapes.md") (start 2 56) (end 2 64) (annotation error) (line-text "\tto_inspect : Nullable(a) -> Str where [a.to_inspect : a -> Str]"))
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
UpperIdent,OpColonEqual,OpenCurly,LowerIdent,OpColon,UpperIdent,NoSpaceOpenRound,UpperIdent,CloseRound,CloseCurly,
UpperIdent,OpDoubleColon,OpenCurly,LowerIdent,OpColon,UpperIdent,NoSpaceOpenRound,UpperIdent,CloseRound,CloseCurly,
LowerIdent,OpColon,UpperIdent,NoSpaceOpenRound,UpperIdent,NoSpaceOpenRound,UpperIdent,CloseRound,CloseRound,OpArrow,UpperIdent,
LowerIdent,OpAssign,OpBar,LowerIdent,OpBar,UpperIdent,NoSpaceDotLowerIdent,NoSpaceOpenRound,LowerIdent,CloseRound,
LowerIdent,OpColon,OpenRound,UpperIdent,Comma,UpperIdent,NoSpaceOpenRound,UpperIdent,CloseRound,CloseRound,OpArrow,UpperIdent,
LowerIdent,OpAssign,OpBar,LowerIdent,OpBar,UpperIdent,NoSpaceDotLowerIdent,NoSpaceOpenRound,LowerIdent,CloseRound,
LowerIdent,OpColon,OpenSquare,UpperIdent,NoSpaceOpenRound,UpperIdent,NoSpaceOpenRound,UpperIdent,CloseRound,CloseRound,Comma,UpperIdent,CloseSquare,OpArrow,UpperIdent,
LowerIdent,OpAssign,OpBar,LowerIdent,OpBar,UpperIdent,NoSpaceDotLowerIdent,NoSpaceOpenRound,LowerIdent,CloseRound,
LowerIdent,OpColon,UpperIdent,NoSpaceOpenRound,UpperIdent,NoSpaceOpenRound,UpperIdent,CloseRound,CloseRound,OpArrow,UpperIdent,
LowerIdent,OpAssign,OpBar,LowerIdent,OpBar,UpperIdent,NoSpaceDotLowerIdent,NoSpaceOpenRound,LowerIdent,CloseRound,
LowerIdent,OpColon,UpperIdent,OpArrow,UpperIdent,
LowerIdent,OpAssign,OpBar,LowerIdent,OpBar,UpperIdent,NoSpaceDotLowerIdent,NoSpaceOpenRound,LowerIdent,CloseRound,
LowerIdent,OpColon,UpperIdent,OpArrow,UpperIdent,
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
		(s-type-decl
			(header (name "Wrapper")
				(args))
			(ty-record
				(anno-record-field (name "note")
					(ty-apply
						(ty (name "Nullable"))
						(ty (name "Str"))))))
		(s-type-decl
			(header (name "Hidden")
				(args))
			(ty-record
				(anno-record-field (name "note")
					(ty-apply
						(ty (name "Nullable"))
						(ty (name "Str"))))))
		(s-type-anno (name "in_list")
			(ty-fn
				(ty-apply
					(ty (name "List"))
					(ty-apply
						(ty (name "Nullable"))
						(ty (name "Str"))))
				(ty (name "Str"))))
		(s-decl
			(p-ident (raw "in_list"))
			(e-lambda
				(args
					(p-ident (raw "v")))
				(e-apply
					(e-ident (raw "Str.inspect"))
					(e-ident (raw "v")))))
		(s-type-anno (name "in_tuple")
			(ty-fn
				(ty-tuple
					(ty (name "I64"))
					(ty-apply
						(ty (name "Nullable"))
						(ty (name "Str"))))
				(ty (name "Str"))))
		(s-decl
			(p-ident (raw "in_tuple"))
			(e-lambda
				(args
					(p-ident (raw "v")))
				(e-apply
					(e-ident (raw "Str.inspect"))
					(e-ident (raw "v")))))
		(s-type-anno (name "in_tag")
			(ty-fn
				(ty-tag-union
					(tags
						(ty-apply
							(ty (name "Some"))
							(ty-apply
								(ty (name "Nullable"))
								(ty (name "Str"))))
						(ty (name "None"))))
				(ty (name "Str"))))
		(s-decl
			(p-ident (raw "in_tag"))
			(e-lambda
				(args
					(p-ident (raw "v")))
				(e-apply
					(e-ident (raw "Str.inspect"))
					(e-ident (raw "v")))))
		(s-type-anno (name "in_box")
			(ty-fn
				(ty-apply
					(ty (name "Box"))
					(ty-apply
						(ty (name "Nullable"))
						(ty (name "Str"))))
				(ty (name "Str"))))
		(s-decl
			(p-ident (raw "in_box"))
			(e-lambda
				(args
					(p-ident (raw "v")))
				(e-apply
					(e-ident (raw "Str.inspect"))
					(e-ident (raw "v")))))
		(s-type-anno (name "in_nominal")
			(ty-fn
				(ty (name "Wrapper"))
				(ty (name "Str"))))
		(s-decl
			(p-ident (raw "in_nominal"))
			(e-lambda
				(args
					(p-ident (raw "v")))
				(e-apply
					(e-ident (raw "Str.inspect"))
					(e-ident (raw "v")))))
		(s-type-anno (name "in_opaque")
			(ty-fn
				(ty (name "Hidden"))
				(ty (name "Str"))))
		(s-decl
			(p-ident (raw "in_opaque"))
			(e-lambda
				(args
					(p-ident (raw "v")))
				(e-apply
					(e-ident (raw "Str.inspect"))
					(e-ident (raw "v")))))))
~~~
# FORMATTED
~~~roc
NO CHANGE
~~~
# CANONICALIZE
~~~clojure
(can-ir
	(d-let
		(p-assign (ident "inspect_reaches_unsatisfied_where_through_shapes.Nullable.to_inspect"))
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
									(e-interpolation (constraint-fn-var 446) (dispatcher-var 37)
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
		(p-assign (ident "in_list"))
		(e-lambda
			(args
				(p-assign (ident "v")))
			(e-call (constraint-fn-var 466)
				(e-lookup-external
					(builtin))
				(e-lookup-local
					(p-assign (ident "v")))))
		(annotation
			(ty-fn (effectful false)
				(ty-apply (name "List") (builtin)
					(ty-apply (name "Nullable") (local)
						(ty-lookup (name "Str") (builtin))))
				(ty-lookup (name "Str") (builtin)))))
	(d-let
		(p-assign (ident "in_tuple"))
		(e-lambda
			(args
				(p-assign (ident "v")))
			(e-call (constraint-fn-var 480)
				(e-lookup-external
					(builtin))
				(e-lookup-local
					(p-assign (ident "v")))))
		(annotation
			(ty-fn (effectful false)
				(ty-tuple
					(ty-lookup (name "I64") (builtin))
					(ty-apply (name "Nullable") (local)
						(ty-lookup (name "Str") (builtin))))
				(ty-lookup (name "Str") (builtin)))))
	(d-let
		(p-assign (ident "in_tag"))
		(e-lambda
			(args
				(p-assign (ident "v")))
			(e-call (constraint-fn-var 495)
				(e-lookup-external
					(builtin))
				(e-lookup-local
					(p-assign (ident "v")))))
		(annotation
			(ty-fn (effectful false)
				(ty-tag-union
					(ty-tag-name (name "Some")
						(ty-apply (name "Nullable") (local)
							(ty-lookup (name "Str") (builtin))))
					(ty-tag-name (name "None")))
				(ty-lookup (name "Str") (builtin)))))
	(d-let
		(p-assign (ident "in_box"))
		(e-lambda
			(args
				(p-assign (ident "v")))
			(e-call (constraint-fn-var 508)
				(e-lookup-external
					(builtin))
				(e-lookup-local
					(p-assign (ident "v")))))
		(annotation
			(ty-fn (effectful false)
				(ty-apply (name "Box") (builtin)
					(ty-apply (name "Nullable") (local)
						(ty-lookup (name "Str") (builtin))))
				(ty-lookup (name "Str") (builtin)))))
	(d-let
		(p-assign (ident "in_nominal"))
		(e-lambda
			(args
				(p-assign (ident "v")))
			(e-call (constraint-fn-var 518)
				(e-lookup-external
					(builtin))
				(e-lookup-local
					(p-assign (ident "v")))))
		(annotation
			(ty-fn (effectful false)
				(ty-lookup (name "Wrapper") (local))
				(ty-lookup (name "Str") (builtin)))))
	(d-let
		(p-assign (ident "in_opaque"))
		(e-lambda
			(args
				(p-assign (ident "v")))
			(e-call (constraint-fn-var 528)
				(e-lookup-external
					(builtin))
				(e-lookup-local
					(p-assign (ident "v")))))
		(annotation
			(ty-fn (effectful false)
				(ty-lookup (name "Hidden") (local))
				(ty-lookup (name "Str") (builtin)))))
	(s-nominal-decl
		(ty-header (name "Nullable")
			(ty-args
				(ty-rigid-var (name "a"))))
		(ty-tag-union
			(ty-tag-name (name "Null"))
			(ty-tag-name (name "NotNull")
				(ty-rigid-var-lookup (ty-rigid-var (name "a"))))))
	(s-nominal-decl
		(ty-header (name "Wrapper"))
		(ty-record
			(field (field "note")
				(ty-apply (name "Nullable") (local)
					(ty-lookup (name "Str") (builtin))))))
	(s-nominal-decl
		(ty-header (name "Hidden"))
		(ty-record
			(field (field "note")
				(ty-apply (name "Nullable") (local)
					(ty-lookup (name "Str") (builtin)))))))
~~~
# TYPES
~~~clojure
(inferred-types
	(defs
		(patt (type "Nullable(a) -> Str where [a.to_inspect : a -> Str]"))
		(patt (type "List(Nullable(Str)) -> Str"))
		(patt (type "(I64, Nullable(Str)) -> Str"))
		(patt (type "[None, Some(Nullable(Str))] -> Str"))
		(patt (type "Box(Nullable(Str)) -> Str"))
		(patt (type "Wrapper -> Str"))
		(patt (type "Hidden -> Str")))
	(type_decls
		(nominal (type "Nullable(a)")
			(ty-header (name "Nullable")
				(ty-args
					(ty-rigid-var (name "a")))))
		(nominal (type "Wrapper")
			(ty-header (name "Wrapper")))
		(nominal (type "Hidden")
			(ty-header (name "Hidden"))))
	(expressions
		(expr (type "Nullable(a) -> Str where [a.to_inspect : a -> Str]"))
		(expr (type "List(Nullable(Str)) -> Str"))
		(expr (type "(I64, Nullable(Str)) -> Str"))
		(expr (type "[None, Some(Nullable(Str))] -> Str"))
		(expr (type "Box(Nullable(Str)) -> Str"))
		(expr (type "Wrapper -> Str"))
		(expr (type "Hidden -> Str"))))
~~~
