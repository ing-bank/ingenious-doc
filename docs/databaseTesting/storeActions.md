# Store Actions

## **storeDBValueinDataSheet**

**Description**: This action will store the value of a specific cell(from specific row and column) from the result of an SQL select statement in the data sheet

**Input Format** : @SheetName:ColumnName , Condition : DatabaseColumnName, ResultSetRowNumber

=== "Usage"

    | ObjectName | Action | Input          | Condition        |
    |------------|----------------|------------------|---|
    | Database   | :green_circle: [`storeDBValueinDataSheet`](#) | DatasheetName:ColumnName  | DatabaseColumnName, ResultSetRowNumber   |

=== "Corresponding Code"

    ```java
    @Action(object = ObjectType.DATABASE, desc = "Save DB value in Test Data Sheet", input = InputType.YES, condition = InputType.YES)
        public void storeDBValueinDataSheet() {
            try {
                if (Condition != null && Input != null) {
                    int rowIndex = 1;
                    result.first();
                    String[] sheetDetail = Input.split(":");
                    String sheetName = sheetDetail[0];
                    String columnName = sheetDetail[1];
                    String value;
                    String[] split = Condition.split(",");
                    if (split.length > 1) {
                        rowIndex = Integer.parseInt(split[1]);
                    }
                    if (!result.absolute(rowIndex)) {
                        Report.updateTestLog(Action, "Row : " + rowIndex + " doesn't exist ", Status.FAILNS);
                    } else if (getColumnIndex(split[0]) != -1) {
                        value = result.getString(split[0]);
                        userData.putData(sheetName, columnName, value);
                        Report.updateTestLog(Action, "Value from DB " + value + "  stored into " + "the data sheet", Status.DONE);
                    } else {
                        Report.updateTestLog(Action, "Column : " + split[0] + " doesn't exist", Status.FAILNS);
                    }
                } else {
                    Report.updateTestLog(Action, "Incorrect Input or Condition format", Status.FAILNS);
                }
            } catch (SQLException ex) {
                Report.updateTestLog(Action, "Error: " + ex.getMessage(), Status.FAILNS);
                System.out.println("Invalid Data " + Condition);
            }
        }

    ```

## **storeValueInVariable**

**Description**: This action will store the value of a specific cell(from specific row and column) from the result of an SQL select statement in a user defined variable

**Input Format** : %variableName% , Condition : DatabaseColumnName,ResultSetRowNumber

=== "Usage"

    | ObjectName | Action |Input        | Condition          |
    |------------|--------------|--------------------|---|
    | Database   | :green_circle: [`storeValueInVariable`](#) | %variableName%        | DatabaseColumnName,ResultSetRowNumber     |

=== "Corresponding Code"

    ```java

    @Action(object = ObjectType.DATABASE, desc = "Store it in the variable from the DB column [<Condition>] ", input = InputType.YES, condition = InputType.YES)
        public void storeValueInVariable() {
            storeValue(Input, Condition, false);
            if (getVar(Input) != null && !getVar(Input).equals("")) {
                Report.updateTestLog(Action, "Stored in the variable", Status.PASSNS);
            } else {
                Report.updateTestLog(Action, "Value doesn't stored in Global variable", Status.FAILNS);
            }
        }

    ```

## **storeValueInGlobalVariable**

**Description**: This action will store the value of a specific cell(from specific row and column) from the result of an SQL select statement in global variable

**Input Format** : %variableName% , Condition : DatabaseColumnName,ResultSetRowNumber

=== "Usage"

    | ObjectName | Action | Input        | Condition       |
    |------------|--------------|-----------------|----|
    | Database   | :green_circle: [`storeValueInGlobalVariable`](#) | %variableName%        | DatabaseColumnName,ResultSetRowNumber  |

=== "Corresponding Code"

    ```java

    @Action(object = ObjectType.DATABASE, desc = "Store it in Global variable from the DB column [<Condition>] ", input = InputType.YES, condition = InputType.YES)
        public void storeValueInGlobalVariable() {
            storeValue(Input, Condition, true);
            if (getVar(Input) != null && !getVar(Input).equals("")) {
                Report.updateTestLog(Action, "Stored in Global variable", Status.PASSNS);
            } else {
                Report.updateTestLog(Action, "Value doesn't stored in Global variable", Status.FAILNS);
            }
        }

    ```

## **storeResultInDataSheet**

**Description**:  This action will store the result of an SQL select statement in the test data sheet

**Input Format** : @`SQL Query` , Condition : DatasheetName

=== "Usage"

    | ObjectName | Action | Input                            | Condition |
    |------------|----------------------------------|-----------|----|
    | Database   | :green_circle: [`storeResultInDataSheet`](#) | ```@select designation from job where id=121;```  | DatasheetName |

=== "Corresponding Code"

    ```java
    @Action(object = ObjectType.DATABASE, desc = "Query and save the result in Datasheet ", input = InputType.YES, condition = InputType.YES)
        public void storeResultInDataSheet() {
            try {
                executeSelect();
                result.last();
                int totalRows = result.getRow();
                result.beforeFirst();
                int totalCols = resultData.getColumnCount();
                for (int colIndex = 0; colIndex < totalCols; colIndex++) {
                    result.beforeFirst();
                    for (int rowIndex = 1; rowIndex <= totalRows; rowIndex++) {
                        if (result.absolute(rowIndex)) {
                            userData.putData(Condition, colNames.get(colIndex), result.getString(colIndex + 1), userData.getIteration(), Integer.toString(rowIndex));
                        } else {
                            Report.updateTestLog(Action, "Row " + rowIndex + " doesn't exist",
                                Status.FAILNS);
                            return;
                        }
                    }
                }
                Report.updateTestLog(Action, " SQL Query Result has been saved in DataSheet: ",
                    Status.PASSNS);
                } catch (SQLException ex) {
                Report.updateTestLog(Action, "Error executing the SQL Query: " + ex.getMessage(),
                    Status.FAILNS);
            }
        }

    ```

## **storeResultInVariable**

**Description**: This action will store the result of an SQL select statement in a user defined variable. The select query in this case should return a single column, the query may return multiple rows. In case the query returns a single value, the value will be stored in the variable name given (for eg:- var), In case if the select query returns multiple rows, multiple variables will be created by adding indexes to the variable name given and the value will be stored in these variables(for eg:- var1, var2, var3.....)

**Input Format** : @`SQL Query` , Condition : %VariableName% 

=== "Usage"

    | ObjectName | Action | Input                             | Condition |
    |------------|-----------------------------------|-----------|----|
    | Database   | :green_circle: [`storeResultInVariable`](#) | ```@@select designation from job where id=121;"```   | %variableName%     |

=== "Corresponding Code"

    ```java
    @Action(object = ObjectType.DATABASE, desc = "Query and save the result in variable(s) ", input = InputType.YES, condition = InputType.YES)
        public void storeResultInVariable() {
            String variableName = Condition;
            try {
                executeSelect();
                result.last();
                int totalRows = result.getRow();
                result.beforeFirst();
                for (int index = 1; index <= totalRows; index++) {
                    if (result.absolute(index)) {
                        if (index == 1) {
                            addVar(variableName, result.getString(1));
                        } else {
                            String temp = variableName.replaceAll("[%]$", index + "%");
                            addVar(temp, result.getString(1));
                        }
                    } else {
                        Report.updateTestLog(Action, "Row " + index + " doesn't exist",
                            Status.FAILNS);
                        return;
                    }
                }
                Report.updateTestLog(Action, " SQL Query Result has been saved in the run time variable(s) ",
                    Status.PASSNS);
            } catch (SQLException ex) {
                Report.updateTestLog(Action, "Error executing the SQL Query: " + ex.getMessage(),
                    Status.FAILNS);
            }
        }
    ```

## **storeDBXMLelementInVariable**

**Description**: This action will evaluate the xml reply for the xpath expressions present in Data/Input - datasheet and store the XML element result into runtime variables. 

**Input Format** : @SheetName:ColumnName  , Condition : %VariableName% 

=== "Usage"

    | ObjectName | Action | Input                             | Condition |
    |------------|-----------------------------------|-----------|----|
    | Database   | :green_circle: [`storeDBXMLelementInVariable`](#) | ```@SheetName:ColumnName```   | %variableName%     |

=== "Corresponding Code"

    ```java
    @Action(object = ObjectType.DATABASE, desc = "Store DB XML Element", input = InputType.YES, condition = InputType.YES)
    public void storeDBXMLelementInVariable() {
        try {
            String variableName = Condition;
            String expression = Data;
            if (variableName.matches("%.*%")) {
                DocumentBuilderFactory dbFactory = DocumentBuilderFactory.newInstance();
                DocumentBuilder dBuilder;
                InputSource inputSource = new InputSource();
                inputSource.setCharacterStream(new StringReader(replybodies.get(key)));
                dBuilder = dbFactory.newDocumentBuilder();
                Document doc = dBuilder.parse(inputSource);
                doc.getDocumentElement().normalize();
                XPath xPath = XPathFactory.newInstance().newXPath();
                NodeList nodeList = (NodeList) xPath.compile(expression).evaluate(doc, XPathConstants.NODESET);
                Node nNode = nodeList.item(0);
                String value = (nNode != null) ? nNode.getTextContent() : null;
                addVar(variableName, value);
                Report.updateTestLog(Action, "DB XML element value stored", Status.DONE);
            } else {
                Report.updateTestLog(Action, "Variable format is not correct", Status.DEBUG);
            }
        } catch (IOException | ParserConfigurationException | XPathExpressionException | DOMException
                 | SAXException ex) {
            Logger.getLogger(this.getClass().getName()).log(Level.OFF, null, ex);
            Report.updateTestLog(Action, "Error Storing DB XML element :" + "\n" + ex.getMessage(), Status.DEBUG);
        }
    }

    ```

## **storeResultDBXMLReplyInVariable**

**Description**: This action will store the result- XML Reply if not null or empty of an SQL select statement in a user defined variable. The select query in this case should return a single column, the query may return multiple rows. In case the query returns a single value, the value will be stored in the variable name given (for eg:- var), In case if the select query returns multiple rows, multiple variables will be created by adding indexes to the variable name given and the value will be stored in these variables(for eg:- var1, var2, var3.....)

**Input Format** : @`SQL Query` , Condition : %VariableName% 

=== "Usage"

    | ObjectName | Action | Input                             | Condition |
    |------------|-----------------------------------|-----------|----|
    | Database   | :green_circle: [`storeResultDBXMLReplyInVariable`](#) | ```@@select reply.xml_message from job where id=121;"```   | %variableName%     |

=== "Corresponding Code"

    ```java
    @Action(object = ObjectType.DATABASE, desc = "Query and save the XMLReply in Datasheet ", input = InputType.YES, condition = InputType.YES)
    public void storeResultDBXMLReplyInVariable() {
        String variableName = Condition;
        try {
            executeSelect();
            result.last();
            int totalRows = result.getRow();
            result.beforeFirst();
            int totalCols = resultData.getColumnCount();
            for (int colIndex = 0; colIndex < totalCols; colIndex++) {
                result.beforeFirst();
                replybodies.clear();
                for (int rowIndex = 1; rowIndex <= totalRows; rowIndex++) {
                    if (result.absolute(rowIndex)) {
                        String xmlReply = result.getString(colIndex + 1);       
                        Integer.toString(rowIndex));
                        String varName = (rowIndex == 1)
                                ? variableName
                                : variableName.replaceAll("[%]$", rowIndex + "%");
                        addVar(varName, result.getString(1));
                        if (xmlReply != null) {
                            replybodies.put(key, xmlReply);
                        }
                    } else {
                        Report.updateTestLog(Action, "Row " + rowIndex + " doesn't exist",
                                Status.FAILNS);
                        return;
                    }
                }
            }
            Report.updateTestLog(Action, " SQL Query Reply has been saved in run time variable(s) ",
                    Status.PASSNS);
        } catch (SQLException ex) {
            Report.updateTestLog(Action, "Error executing the SQL Query: " + ex.getMessage(),
                    Status.FAILNS);
        }

    }
    ```

## **storeDBXMLelementListInDataSheet**

**Description**: This action will store the XML element- single or list of XML element values into the specified Datasheet. 

**Input Format** : @SheetName:ColumnName  , Condition : %VariableName% 

=== "Usage"

    | ObjectName | Action | Input                             | Condition |
    |------------|-----------------------------------|-----------|----|
    | Database   | :green_circle: [`storeDBXMLelementListInDataSheet`](#) | ```SheetName:ColumnName```   | %variableName%     |

=== "Corresponding Code"

    ```java
    @Action(object = ObjectType.DATABASE, desc = "Store DB XML ElementList In DataSheet", input = InputType.YES, condition = InputType.YES)
    public void storeDBXMLelementListInDataSheet() {
        try {
            String strObj = Input;
            if (strObj.matches(".*:.*")) {
                try {
                    System.out.println("Updating value in SubIteration " + userData.getSubIteration());
                    String sheetName = strObj.split(":", 2)[0];
                    String columnName = strObj.split(":", 2)[1];
                    String xmlText = replybodies.get(key);
                    if (xmlText == null) {
                        Report.updateTestLog(Action, "No XML found for key: " + key, Status.DEBUG);
                        return;
                    }
                    DocumentBuilderFactory dbFactory = DocumentBuilderFactory.newInstance();
                    DocumentBuilder dBuilder = dbFactory.newDocumentBuilder();
                    InputSource inputSource = new InputSource(new StringReader(xmlText));
                    Document doc = dBuilder.parse(inputSource);
                    doc.getDocumentElement().normalize();
                    XPath xPath = XPathFactory.newInstance().newXPath();
                    String[] expressions;
                    if (Condition != null && (Condition.startsWith("%") || Condition.endsWith("%"))) {
                        expressions = getVar(Condition).split(";");
                    } else {
                        expressions = Condition.split(";");
                    }
                    List<String> values = new ArrayList<>();
                    for (String expr : expressions) {
                        expr = expr.trim();
                        if (!expr.isEmpty()) {
                            System.out.println("Evaluating XPath Expression: " + expr);
                            NodeList nodeList = (NodeList) xPath.compile(expr).evaluate(doc, XPathConstants.NODESET);
                            Node nNode = (nodeList != null && nodeList.getLength() > 0) ? nodeList.item(0) : null;
                            String value = (nNode != null && nNode.getTextContent() != null) ? nNode.getTextContent().trim() : "";
                            values.add(value);
                        } else {
                            values.add(""); 
                        }
                    }
                    String combinedValue = String.join(";", values);
                    System.out.println("Combined value: " + combinedValue);            
                    userData.putData(sheetName, columnName, combinedValue);
                    Report.updateTestLog(Action, "Element texts [" + combinedValue + "] stored in " + strObj, Status.DONE);
                } catch (IOException | ParserConfigurationException | XPathExpressionException | DOMException |
                         SAXException ex) {
                    Logger.getLogger(this.getClass().getName()).log(Level.OFF, ex.getMessage(), ex);
                    Report.updateTestLog(Action, "Error storing DB XML element List in datasheet:\n" + ex.getMessage(), Status.DEBUG);
                }
            } else {
                Report.updateTestLog(Action,
                        "Given input [" + Input + "] format is invalid. It should be [sheetName:ColumnName]",
                        Status.DEBUG);
            }
        } catch (Exception ex) {
            Logger.getLogger(this.getClass().getName()).log(Level.OFF, null, ex);
            Report.updateTestLog(Action, "Error storing DB XML element List in datasheet:\n" + ex.getMessage(), Status.DEBUG);
        }
    }
    ```
