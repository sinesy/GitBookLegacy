A scheduled process can be defined starting from a server-side js action.
That action should not use predefined variables such as username or companyId, etc since a scheduled process is not connected to a specific user, unless when you define a scheduled process you also specify a user to connect to that process: in that case, the server-side js action would inherit the user&#8217;s settings.
It is important to pass back to the scheduler manager the outcome of the action execution, so that the scheduler can store the outcome in the history of the executions.
This can be accomplished using the following instructions:
var result = {
exitCode: &#8220;0&#8221;,
exitMessage: &#8220;&#8221;
};
utils.setReturnValue(JSON.stringify(result));

Suppose you want to inform the scheduler that something was wrong, you could send back the following response:
var result = {
exitCode: &#8220;-1&#8221;,
exitMessage: &#8220;This is the message to pass back to the scheduler&#8221;
};
utils.setReturnValue(JSON.stringify(result));


                

---


