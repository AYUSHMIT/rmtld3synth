

# rmtld3synth tool: Generating monitors from a fragment of MTL with durations


## Using RMTLD3 synthesis tool to generate monitors

RMTLD3 synthesis tool allows us to automatically generate monitors based on the formal specification language RMTLD3. RMTLD3 is a three-valued restricted metric temporal logic with durations that is able to reason about explicit time.

Polynomial inequalities are supported by this formalism as well as the common operators of temporal logics. Quantification over formulas is also available as a manner to decompose quantified formulas into several monitoring conditions.

Lets overview a simple monitoring case generation. Before start, we begin with the description of the synthesis settings, and then, we describe the interface of the monitor with the SUO. In that phase, we use a simple test case that is automatically generated by our synthesis tool as a demo.

### Overview of the configuration settings

Settings for RMTLD3 synthesis tool are described using the syntax `(<setting_id> <bool_type | integer_type | string_type>)`, where '|' indicates the different types of arguments such as boolean, integer or string, and `setting_id` the setting identifier of type string.

See [the overall parameters](rmtld3_parameters.md) for more details.

~~~~~~~~~~~~~~~~~~~~~{.lisp}
(gen_tests true)

(minimum_inter_arrival_time 102)
(maximum_period 2000000)
(event_subtype uint_8)
(cluster_name monitor_set1)

(m_simple 1000000 (Or (Until 200000 (Prop A) (Prop C)) (Prop B)))
(m_morecomplex 500000 (Or (Until 200000 (Prop set_off) (Or (Until 200 (Prop A) (Prop C)) (Prop B))) (Prop B)))

~~~~~~~~~~~~~~~~~~~~~

`gen_tests` sets the automatic generations of test cases (to be used as a demo in the described illustration below).

`minimum_inter_arrival_time` establishes the minimum inter-arrival time that the events can have. It is a very pessimistic setting but provides some information for static checking.

`maximum_period` sets the minimum inter-arrival time. It has a correlation between the periodic monitor and the minimum inter-arrival time. It provides static checks according to the size of time-stamps of events.

`event_subtype` provides the type for the event data. In that case, it is an identifier that can distinct 255 events. However, if more events are required, the type should be modified to *uint32_t* or greater. The number of different events versus the available size for the identifier is also statically checked.

`cluster_name` identifies the set of monitors. It acts as a label for grouping monitor specifications.

### Writing formulas in RMTLD3

The formulas `m_simple` and `m_morecomplex` follow the same syntax defined in the paper [[3]](http://link.springer.com/chapter/10.1007%2F978-3-319-23820-3_11).

Let \f$\mathcal{P}\f$ be a set of propositions and \f$\mathcal{V}\f$ a set of logic variables. The syntax of RMTLD3 terms \f$\eta\f$ and formulas \f$\varphi\f$ is defined inductively as follows:

\f{align}{
&\eta \ ::= \ \alpha \ | \ x  \ | \ \eta_1 \circ \eta_2 \ | \ \int^\eta \varphi \nonumber \\
&\varphi \ ::= \ p \ | \ \eta_1 < \eta_2 \ | \ \varphi_1 \lor \varphi_2 \ | \ \neg \varphi \ | \ \varphi_1 \, U_{ \sim \gamma} \, \varphi_2 \ | \ 
\exists x \, \varphi \nonumber \f}


where \f$\alpha\in R\f$, \f$x \in \mathcal{V}\f$ is a logic
variable, \f$\circ\f$ means the arithmetic operators \f$+\f$ and \f$\times\f$,
\f$\int^{\eta} \varphi\f$ is the duration of the formula \f$\varphi\f$ in an
interval, \f\f$p \in \mathcal{P}\f$ is an atomic proposition, \f$U\f$ is a temporal operator with \f$\sim \in \{<,=\}\f$,
\f$\gamma \in R_{\geq0}\f$, and the meaning of \f$\eta_1 < \eta_2, \varphi_1 \lor \varphi_2, \neg \varphi, \exists x \, \varphi\f$ is defined as usual.

[TODO]

#### Illustrating the unit test generation

[TODO]
