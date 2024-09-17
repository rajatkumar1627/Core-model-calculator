# Core Model Calculator

## Overview
The **Core Model Calculator** is a web-based application that allows users to input a core model (in a specified format) and calculates various parameters such as:
- Core Factor
- Effective Volume
- Effective Length
- Effective Area
- Minimum Area

The application consists of a Java backend (Servlet-based) and a simple frontend that interacts with the backend to retrieve the results based on the core model dimensions.

## Table of Contents
- [Overview](#overview)
- [Technologies Used](#technologies-used)
- [Project Structure](#project-structure)
- [Core Model Format](#core-model-format)
- [Features](#features)
- [API Endpoints](#api-endpoints)
- [How to Run](#how-to-run)
- [Example Usage](#example-usage)
- [Troubleshooting](#troubleshooting)

## Technologies Used
- **Java Servlet API** for handling requests
- **Google Gson** for JSON conversion
- **HTML, CSS, and JavaScript** for the frontend
- **Fetch API** to send HTTP requests from the frontend to the backend
- **Apache Tomcat** for deployment

## Project Structure

```
CoreModelCalculator/
│
├── src/
│   ├── main/
│   │   ├── java/com/example/
│   │   │   ├── CoreModelCalculator.java    # Core model calculation logic
│   │   │   ├── ServletController.java      # Servlet to handle API requests
│   │   └── webapp/
│   │       ├── WEB-INF/
│   │       │   └── web.xml                 # Servlet mapping configuration
│   │       ├── index.html                  # Frontend interface
│   │       └── script.js                   # JavaScript logic for interacting with backend
│   └── test/                               # Unit test directory (optional)
│
├── pom.xml                                 # Maven configuration file
├── README.md                               # This README file
└── .gitignore
```

## Core Model Format

The core model should follow a specific format:
```
EE25/13/7
```
This format represents:
- **Outer Diameter**: First part after the prefix (e.g., `25` in `EE25`)
- **Inner Diameter**: Second part (e.g., `13`)
- **Height**: Third part (e.g., `7`)

## Features
- **Core Factor Calculation**: Calculates the core factor based on the input model.
- **Effective Volume Calculation**: Computes the effective volume of the core.
- **Effective Length Calculation**: Calculates the effective length based on the core model dimensions.
- **Effective Area Calculation**: Computes the effective area.
- **Minimum Area Calculation**: Calculates the minimum area.

## API Endpoints

### 1. `/calculate` (POST)
- **Description**: Calculate various parameters based on the provided core model.
- **Request**:
  - `Content-Type`: `application/x-www-form-urlencoded`
  - `body`: 
    ```
    coreModel=EE25/13/7
    ```
- **Response**:
  - `Content-Type`: `application/json`
  - Example successful response:
    ```json
    {
        "coreFactor": 11.0966,
        "effectiveVolume": 28.6932,
        "effectiveLength": 8.5268,
        "effectiveArea": 42.0000,
        "minimumArea": 13.2725
    }
    ```
  - Example error response:
    ```json
    {
        "error": "Error: Invalid core model format: EE25-13-7\nStack trace: ..."
    }
    ```

### 2. `/calculate` (GET)
- **Description**: A simple health check to confirm that the servlet is running.
- **Response**:
  - `Content-Type`: `text/plain`
  - Example response: 
    ```
    Calculator servlet is running
    ```

## How to Run

### Prerequisites
- **Java 8+**
- **Apache Tomcat** or any other servlet container
- **Maven** for dependency management

### Steps

1. **Clone the Repository**:
   ```bash
   git clone https://github.com/your-repo/core-model-calculator.git
   cd core-model-calculator
   ```

2. **Build the Project**:
   Ensure Maven is installed. Run the following command to build the project and resolve dependencies:
   ```bash
   mvn clean package
   ```

3. **Deploy the WAR File**:
   After building, the WAR file will be generated in the `target/` directory. Deploy this WAR file to your servlet container (e.g., Apache Tomcat).

4. **Access the Application**:
   Once deployed, access the application by navigating to `http://localhost:8080/core-model-calculator-1.0-SNAPSHOT/` in your browser.

### Local Testing
You can run the servlet locally on an embedded Tomcat server or any other servlet container. Access the servlet at `/calculate`.

## Example Usage

1. **Input Example**:
   Open the web interface and enter the core model in the form `EE25/13/7`.

2. **Expected Output**:
   Once submitted, the calculated values will be displayed on the page:
   ```
   Core Factor: 11.0966
   Effective Volume (Ve): 28.6932 cm³
   Effective Length (le): 8.5268 cm
   Effective Area (Ae): 42.0000 cm²
   Minimum Area (An): 13.2725 cm²
   ```

## Troubleshooting

### Common Issues

1. **500 Internal Server Error**:
   - Check the server logs to identify the root cause.
   - Ensure that the input format is correct (e.g., `EE25/13/7`).
   - Ensure that all required dependencies are included and properly configured.

2. **Core Model Parsing Error**:
   - If the core model string is in an incorrect format (e.g., `EE25-13-7` instead of `EE25/13/7`), an `IllegalArgumentException` will be thrown. Ensure the core model input follows the correct format.

### Debugging Tips
- **Logging**: Use `System.out.println()` to log incoming requests, parsed values, and error messages.
- **Stack Traces**: Review any stack traces that are logged to the console to identify parsing or calculation issues.

## License
This project is licensed under the MIT License. See the [LICENSE](LICENSE) file for more details.
---

This README file gives an in-depth explanation of the project, its structure, how to run it, and how to troubleshoot common issues.
