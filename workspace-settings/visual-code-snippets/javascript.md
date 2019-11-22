# Javascript

## 11/22/2019

```javascript
{
	//#region Huron Portal
	"ApplicationEntity.getResultSet().query()": {
		"prefix": "portalq",
		"body": [
			"var eType = \"${1:eType}\"",
			"var queryString = \"${2:queryString}\";",
			"var queryResults = ApplicationEntity.getResultSet(eType).query(queryString);",
			"log(CustomUtils.uga_findOne(eType, queryString));",
			"//if (queryResults && queryResults.count > 0) {",
			"//\tvar enum = queryResults.elements();",
			"",
			"//} else {",
			"//\tlog(\"No Results Found\")",
			"//}",
			"",
			"function log(x) {",
			"\t?x + \"\\n\"",
			"}"
		],
		"description": "Portal Queries"
	},
	"Inner Portal Function": {
		"prefix": "innerfunc",
		"body": [
			"/**",
			" * @description",
			" * @returns",
			" */"
			"function ${1:functionName}() {",
			"\tvar INNER_DEBUG = true;",
			"\tif (DEBUG && INNER_DEBUG) log(\"DEBUG\", \"${1:functionName}() beginning: \");",
			"\ttry {",
			"\t"
			"\t} catch (e) {",
			"\t\tlog(\"ERROR\", \"${1:functionName}(): \" + e.description);",
			"\t\tthrow e;",
			"\t}",
			"}"
		],
		"description": "The 'Best Practices' version of a custom method try/catch block",
	},
	"Portal Function": {
		"prefix": "portalfunc",
		"body": [
			"/**",
			" * @description $1",
			" * @param {Object} argumentObject - not currently used. Leaving for potential future need.",
			" * @returns {undefined}",
			" */"
			"function ${2:functionName}(argumentObject) {"
			"\tvar DEBUG = true;",
			"\tvar PREFIX = \"[${3:Entity Type}](${2:functionName}): \";",
			"\t//? Use like: log(\"DEBUG\", \"Debug message goes here\") or log(\"INFO\", \"Info Message goes here\")"
			"\tvar log = createLoggerForPrefix(PREFIX);",
			"",
			"\ttry {",
			"",
			"\t\t//* Assertions and Declarations",
			"",
			"\t\tif (DEBUG) log(\"DEBUG\", \"Passed Assertion Block\");",
			"",
			"\t\t//* Execution",
			"",
			"\t\t//* Functions",
			"",
			"\t\t/**",
			"\t\t * @description uses the defined PREFIX to create a logging function that will concatenate the log level,",
			"\t\t * the prefix, and the message. ",
			"\t\t * @param {String} PREFIX - [Entity Type](methodName)",
			"\t\t * @returns {Function}",
			"\t\t */",
			"\t\t\tfunction createLoggerForPrefix(PREFIX) {",
			"\t\t\t/**",
			"\t\t\t * @param {String} logLevel - \"DEBUG\", \"INFO\", \"ERROR\", \"WARN\"",
			"\t\t\t * @param {String} message",
			"\t\t\t * @returns {undefined}",
			"\t\t\t */",
			"\t\t\treturn function logger(logLevel, message) {",
			"\t\t\t\tlogLevel = logLevel || \"DEBUG \";",
			"\t\t\t\twom.log(logLevel.match(/\\S.*\\S/g)[0] + \" \" + PREFIX.match(/\\S.*\\S/g)[0] + \" \" + message);",
			"\t\t}",
			"\t\t};",
			"",
			"\t} catch (e) {",
			"\t\tlog(\"ERROR\", e.description);",
			"\t\tthrow e;",
			"\t}",
			"}"
		],
		"description": "portal function setup",
	},
	"wom.log()": {
		"prefix": "womlog",
		"body": [
			"if (DEBUG) wom.log(DEBUG_PREFIX + \"$1\");"
		],
		"description": "wom.log() debug statement"
	},
	"wom.log() a variable value": {
		"prefix": "womvalue",
		"body": [
			"if (DEBUG) wom.log(DEBUG_PREFIX + \"variable '$1' is: \" + $1);"
		],
		"description": "for logging specific variable values"
	},
	"TaskFactory.StartNew()": {
		"prefix": "TaskF",
		"body": [
			"TaskFactory.StartNew(",
			"\t\"${1:queueName}\",",
			"\t\"${2:description}\",",
			"\t${3:workItems},",
			"\tPerson.getCurrentUser(),",
			"\t\"${5:actionMethodName}\",",
			"\t${6:actionMethodContext},",
			"\t${7:arguments}",
			");"
		],
		"description": "TaskFactory.StartNew()"
	},
	"customAttributes": {
		"prefix": "customAttributes",
		"body": [
			"customAttributes"
		]
	},
	"portal console toJSON": {
		"prefix": "consolejson",
		"body": [
			"?JSON.stringify(",
			"\tCustomUtils.uga_toJSON(",
			"\t\t$1,",
			"\t\t// EntityUtils.getObjectFromString(\"\"),",
			"\t\t// CustomUtils.uga_findOne( x, \"\"),",
			"\t\ttrue,",
			"\t\tnull",
			"\t),",
			"\tnull,",
			"\t'\t'",
			")"
		],
		"description": "for use in the portal console"
	},
	"portal script hook": {
		"prefix": "portalprocessing",
		"body": [
			"/**",
			" * @description",
			" */",
			"try {",
			"\tvar DEBUG = true;",
			"\tvar DEBUG_PREFIX = \"DEBUG [$1]($2): \";",
			"",
			"\t$3",
			"",
			"} catch (e) {",
			"\twom.log(DEBUG_PREFIX + \"ERROR - \" + e.description);",
			"\tthrow e;",
			"}"
		],
		"description": "post processing script"
	},
	//#endregion Huron Portal

	//#region Node.js
	"package.json": {
		"prefix": "packagejson",
		"body": [
			"{",
			"\t\"name\": \"modulepractice\",",
			"\t\"version\": \"1.0.0\",",
			"\t\"description\": \"\",",
			"\t\"main\": \"index.js\",",
			"\t\"scripts\": {",
			"\t\t\"test\": \"echo \\\"Error: no test specified\\\" && exit 1\",",
			"\t\"start\": \"node --experimental-modules .\\index.js\"",
			"\t},",
			"\t\"keywords\": [],",
			"\t\"type\": \"module\",",
			"\t\"author\": \"phillip dodd\",",
			"\t\"license\": \"ISC\"",
			"}"
		],
		"description": ""
	}
	//#endregion Node.js
}
```

