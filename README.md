## Splunk: `splunk`

### Overview
Splunk is used for centralized logging and monitoring of transactions. The `splunk` directory contains configuration files to set up Splunk, including certificates, configuration files, and mock data for testing purposes.

### How to Set Up Splunk for Local Testing

1. **Ensure that you have a local Splunk instance running**:
   - If you haven't already, you can download and install Splunk from the [official Splunk website](https://www.splunk.com/).
   - Once installed, start your Splunk instance.

2. **Login to your local Splunk instance**:
   - Open your browser and navigate to `http://localhost:8000` (or whichever port your local Splunk instance is using).
   - Login using your credentials (default is usually `admin`/`adminadmin1` if you haven't changed it).

3. **Load the Mock Data**:
   - In the `splunk` directory, you will find a file named `fakedata.csv`, which contains mock transaction logs.
   - To load the mock data into Splunk:
     1. From the Splunk dashboard, go to **Settings** > **Data Inputs**.
     2. Click on **Files & Directories** and then **Add Data**.
     3. Choose **Upload** and select the `fakedata.csv` file from the `splunk` directory.
     4. Follow the prompts to index the data. You can choose the default index or create a new one.
     5. Once indexed, the data from `fakedata.csv` will be available for viewing and querying in Splunk.

4. **Update Splunk Configuration**:
   - Navigate to the `splunk/default.yml` file and ensure the configuration matches your Splunk setup. This includes setting the correct **host**, **index**, and any authentication details required for connecting to Splunk.

5. **View the Data**:
   - Once the data is loaded and indexed, you can start querying and visualizing the transaction logs in Splunk.
   - Use the **Search & Reporting** app within Splunk to search for logs and analyze them.

6. **(Optional) Use SSL Certificates for Secure Communication**:
   - If you're using secure communication, ensure that you have placed the required certificates in the `splunk/certificates/` directory.


### How to set up Correlation Dashboard Demo

1. Login to Splunk under http://localhost:8000. Username: admin, Password: adminadmin1
2. Install Network Diagram Viz.

On the main board choose "Find more apps". Search for Network Diagram Viz and continue with default installation.

3. Load fake data.

The data that you can find under splunk/mockdata.csv is loaded to the Splunk's containter. However it has to be manually loaded to the application itself. In order to achieve that:

On the right top corner choose Settings >> DATA >> Data Inputs >> File & Directories >> New Local File & Directory

In the "File or Directory" input choose the mockdata from the path /data/mockdata.csv and submit the data with default options.

Now you will able to search that data with the search queries like:

source="/data/mockdata.csv" host="993627bb7161" sourcetype="csv"

4. Create the CorrelationId Tracking Dashboard

Go to Search and Report >> Dashboards >> Create New Dashboard

Copy and paste code from the dashoard.yaml file. Choose Classic Dashboard. Later:

Edit Dashboard >> Source >> Paste the code


---

### Troubleshooting
- If you do not see the mock data after loading it, make sure the indexing process was successful and that you are querying the correct index.
- Double-check the configuration in `splunk/default.yml` for any discrepancies in host or index settings.

---

## Docker Compose Setup

To run the entire stack (backend, frontend, and Splunk) using Docker Compose:

1. Ensure that Docker and Docker Compose are installed.
2. In the project root directory (where `docker-compose.yml` is located), run:

   ```bash
   docker-compose up --build
   ```

3. This will build and start all the services, including the backend, frontend, and Splunk container.
4. The services will be available at:
   - Splunk UI (if configured): `http://localhost:8000`

---
## Troubleshooting

- **Splunk configuration**: Double-check that the certificates are correctly placed in the `splunk/certificates/` directory and that the `splunk/default.yml` file has the correct details.

---

## License

This project is licensed under the MIT License - see the [LICENSE](LICENSE) file for details.