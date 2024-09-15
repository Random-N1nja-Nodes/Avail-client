# Avail-client

## Step 1: Install Rust

Avail’s light client is written in Rust. To install Rust on your machine:

Run the following command to install Rust using the rustup tool:

```
curl --proto '=https' --tlsv1.2 -sSf https://sh.rustup.rs | sh
```

Follow the on-screen instructions to complete the installation.

Once installed, ensure rustup and cargo (Rust’s package manager) are working correctly by checking the version:

```
rustup --version
cargo --version
```

This should display the installed version of rustup and cargo.

If Rust is already installed, make sure it’s up to date:

```
rustup update
```

## Step 2: Clone the Avail Light Client Repository

To set up the light client, you need to clone the Avail repository from GitHub.

First, navigate to the directory where you want to clone the repository:

```
cd <your-desired-directory>
```

Clone the Avail repository by running:

```
git clone https://github.com/availproject/avail-light.git
```

Navigate into the project directory:

```
cd avail-light
```
## Step 3: Build the Light Client

Once you have cloned the repository, you need to compile the light client.

To compile the project, run the following command inside the avail-light directory:

```
cargo build --release
```

This command will download all the necessary dependencies and compile the light client. The --release flag ensures that the binary is optimized for performance.

After the build process is complete, the compiled binary will be located in the target/release directory.

## Step 4: Configure the Light Client

Before running the light client, ensure it’s properly configured.

In the avail-light repository, locate the configuration files. These files contain necessary settings such as network parameters, node addresses, and other runtime options.

Edit the configuration file if necessary, ensuring it points to the correct full nodes and network you intend to connect with. The default configuration is generally sufficient for most use cases.

Example configuration file can be located at config/light-client-config.toml:

```
[network]
bootnodes = ["<node-address>"]
```


Ensure the bootnodes field contains valid addresses of Avail full nodes.

## Step 5: Run the Light Client

Once everything is set up, you are ready to run the light client.

Navigate to the target/release directory:

```
cd target/release
```


Run the light client using the compiled binary:

```
./avail-light --config <path-to-config-file>
```

Replace <path-to-config-file> with the actual path to the configuration file if it's not located in the default directory.

The light client will now connect to the Avail network and begin synchronizing. Since it’s a light client, it will only download the essential headers and proofs, rather than the entire blockchain data.

## Step 6: Monitor the Light Client

While running the light client, it’s important to monitor its performance and ensure it stays connected to the network.

The light client will output logs to the terminal, showing its connection status, synchronization progress, and any potential errors.

You can also configure logging options in the configuration file to control the verbosity and destination of logs (e.g., saving logs to a file).

## Step 7: Interact with the Light Client

Once the light client is running, you can interact with it by sending queries, transactions, or other commands depending on your use case. Light clients are primarily used for:

Verifying state proofs.

Submitting transactions to the network.

Querying blockchain data without full node overhead.

You can also use available RPC (Remote Procedure Call) commands to interact programmatically.

Optional: Running the Light Client as a Service

If you want to run the light client continuously, it’s a good idea to set it up as a background service.

On Linux:

Create a systemd service file for the light client:

```
sudo nano /etc/systemd/system/avail-light.service
```


Add the following content to the file:

```
[Unit]
Description=Avail Light Client
After=network.target

[Service]
ExecStart=/path/to/avail-light --config /path/to/config-file
Restart=on-failure
User=<your-username>
WorkingDirectory=/path/to/avail-light

[Install]
WantedBy=multi-user.target
Save the file and exit.
```


Enable and start the service:

```
sudo systemctl enable avail-light
sudo systemctl start avail-light
```

This setup will run the light client in the background and restart it automatically if it crashes.

Troubleshooting

Here are a few common issues you might encounter:

Build errors: Ensure that all dependencies are installed and that you are using an updated version of Rust.

Connection issues: Check the bootnodes addresses in your configuration file and ensure your machine has a stable internet connection.

Performance problems: Although light clients are designed to be resource-efficient, performance may vary depending on your machine’s specs and the network connection.
