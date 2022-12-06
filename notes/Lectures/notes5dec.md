# Lecture: 5 december

Gui Mimic: recording interaction in the GUI and then recreating it with modification.

WinAfl: Port of Afl for Windows (it's okay as far as it goes - Mike). It expects to interact with a binary with stdin stdout. 

Winnie: an attempt to fuzz gui application, without the problems with interaction with the GUI. You sometimes need to retry, because of the flow starts at some point. This requires a lot of CPU time and memory. Using a harness is extracting the code you need, wrap it and use it as a tiny executable, so you don't need the entire program. You needed to have the source code for this.   
Another way of doing is, is trying the force the application by repeatingly repeating one function. This is completely doable in Linux using a fork, but Windows doesn't have this. What Winnie does this is creating a Windows forks server. Probably the best new idea I've seen in a long time - Mike. It FOSS, but it's abandoned!! (LOL).

