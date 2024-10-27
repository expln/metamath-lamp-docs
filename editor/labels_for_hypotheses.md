# Labels for hypotheses

Metamath-lamp applies some restrictions to what labels can be used for hypothesis steps and for the goal step.
Existing labels in the loaded database, and also existing math symbols 
cannot be used as labels for hypothesis steps and for the goal step. This is justified by the fact that when 
you export the proof from the Editor, that proof will contain those labels "as is", so they will clash with existing
labels and math symbols, but this is not allowed by Metamath syntax rules.

This may cause some problems for users. To improve user experience Metamath-lamp has some automations related to 
labels.

For steps with numeric labels, when you change `P` step type to `H` then:
* if there is the goal step, then the new label will be `the goal step name` + `.` + `Integer`.
* if there is no goal step, then Metamath-lamp checks if the currently assigned label is valid. 
If it is valid, then nothing is changed. If it is invalid then another numeric valid label is generated.

Another feature is the "Rename hypotheses", available in the "hamburger" menu in the Editor. It can automatically
re-label all hypotheses. New labels will be: `the goal step name` + `.` + `Integer`.