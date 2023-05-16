# 🏥 Hospital API

The Hospital API project is a web-based application developed using Node.js and MongoDB. The primary goal of this project is to provide doctors with a platform where they can register, login, and manage patient reports. The application ensures that only registered doctors can create a patient's report and view all reports. Patients, on the other hand, cannot register themselves.

The project has various endpoints that doctors can use to perform different operations. For example, the registration endpoint allows new doctors to create an account by providing their name, email address, and password. Once registered, the doctor can log in and access other functionalities, such as adding new patients, creating reports for them, and viewing all their reports.

To ensure the security of the system, the application employs different authentication techniques such as JSON Web Tokens (JWT) to generate tokens that doctors can use to access various endpoints.

## API Reference

#### Doctor registration

```http
  POST /api/v1/doctors/register
```

| Body       | Type     | Description                      |
| :--------- | :------- | :------------------------------- |
| `name`     | `string` | **Required**. Your full name     |
| `email`    | `string` | **Required**. Your email address |
| `password` | `string` | **Required**.                    |

#### Doctor login

```http
  POST /api/v1/doctors/login
```

| Body       | Type     | Description                      |
| :--------- | :------- | :------------------------------- |
| `email`    | `string` | **Required**. Your email address |
| `password` | `string` | **Required**.                    |

Returns a token valid for 11 days.

#### Patient Register

```http
  POST /api/v1/patients/register
```

| Body     | Type     | Description                        |
| :------- | :------- | :--------------------------------- |
| `name`   | `string` | **Required**. Patient full name    |
| `number` | `number` | **Required**. Patient Phone number |

| Headers         | Type     | Description                |
| :-------------- | :------- | :------------------------- |
| `Authorization` | `string` | **Required**. Bearer Token |

#### Create Patient Report

```http
  POST /api/v1/patients/:id/create_report
```

| Parameter | Type     | Description                                 |
| :-------- | :------- | :------------------------------------------ |
| `id`      | `string` | **Required**. Id of patient to be generated |

| Body     | Type     | Description                     |
| :------- | :------- | :------------------------------ |
| `status` | `string` | **Required**. Status of patient |

| Headers         | Type     | Description                |
| :-------------- | :------- | :------------------------- |
| `Authorization` | `string` | **Required**. Bearer Token |

#### Get all reports of a particular patient

```http
  GET /api/v1/patients/:id/all_reports
```

| Parameter | Type     | Description                               |
| :-------- | :------- | :---------------------------------------- |
| `id`      | `string` | **Required**. Id of patient to be fetched |

| Headers         | Type     | Description                |
| :-------------- | :------- | :------------------------- |
| `Authorization` | `string` | **Required**. Bearer Token |

#### Get all reports of all patients with a specific status

```http
  GET /api/v1/reports/:status
```

| Parameter | Type     | Description                  |
| :-------- | :------- | :--------------------------- |
| `status`  | `string` | **Required**. Specify status |

| Headers         | Type     | Description                |
| :-------------- | :------- | :------------------------- |
| `Authorization` | `string` | **Required**. Bearer Token |

## Features

- There can be 2 types of Users
  - Doctors 🩺
  - Patients 😷
- Doctors can log in
- Each time a patient visits, the doctor will follow 2 steps
  - Register the patient in the app (using phone number, if the patient already exists, just return the patient info in the API)
- After the checkup, create a Report
- Patient Report will have the following fields
  - Created by doctor
  - Status Can be either of: [Negative, Travelled-Quarantine, Symptoms-Quarantine, Postive-Admit etc]
  - Date

## Run Project Locally

Clone the project

```bash
  git clone https://github.com/agarwalshashankjan/HospitalAPI.git
```

Go to the project directory

```bash
  cd HospitalAPI
```

Install the packages

```bash
  npm install
```

```bash
  npm install mongoose dotenv
```

Keep the mongoose server ON and then start the server

To Start the server

```bash
  npm start
```

Check the console for this, if it says connected, the configuration is complete, otherwise resolve the errors:

```mongodb://0.0.0.0/hospitalapi
Server running at http://localhost:8000/
Successfully connected to the database
```
