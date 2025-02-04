# TRON Blockchain Transaction Processor

## 📌 Overview
This project is designed to fetch, filter, and process transactions from the TRON blockchain using the TRON Full Node. It efficiently retrieves and processes transaction data, filters transactions related to blacklist events, and stores the results in a CSV file for further analysis.

## 🚀 Features
- 📡 Fetches transaction data from TRON blocks via API requests.
- 🔄 Converts TRON addresses from hex to base58 format.
- ✅ Filters transactions to include only successful ones.
- 🔍 Detects blacklist-related transactions (Added/RemovedBlackList events).
- 💾 Caches transaction data in memory to improve performance.
- 📊 Saves processed transactions into CSV files for further analysis.
- ⚡ Supports multi-threaded processing for efficiency.

## 🛠 Installation
Ensure you have Python 3 installed. Then install the required dependencies:
```sh
pip install requests pandas tqdm numpy base58 psutil
```

## 🎯 Usage
### Running the Script
To run the script and start processing blocks:
```sh
python script.py
```

### Configuration
Modify the following parameters as needed:
- `batch_size`: Number of blocks to process in each batch.
- `block_last`: Starting block number.
- `max_workers`: Number of concurrent threads for processing.

### 🔎 Filtering Transactions
The script filters transactions based on predefined event signatures:
- **AddedBlackList**: `42e160154868087d6bfdc0ca23d96a1c1cfa32f1b72ba9ba27b69b98a0d819dc`
- **RemovedBlackList**: `d7e9ec6e6ecd65492dce6bf513cd6867560d49544421d0783ddf06e76c24470c`

### 💾 Saving Transactions
Processed transactions are saved in CSV format, with filenames based on block ranges (e.g., `aggregated_transactions-<block_last>.csv`).

### 🗑 Clearing Cache
To clear the in-memory cache, the script calls:
```python
cache.clear_cache()
```
This ensures efficient memory usage during long runs.

## ⚡ Multi-threading Optimization
The script dynamically determines optimal thread usage based on CPU and memory availability:
```python
num_cores = os.cpu_count()
available_memory = psutil.virtual_memory().available / (1024 * 1024)
max_workers = min(num_cores * 2, available_memory // 100)
```

## 📜 Example Workflow
```python
cache = BlockTransactionCache()
block_last = 58000000
batch_size = 10000
while block_last < 58500000:
    process_batch(cache, block_last, batch_size)
    block_last += batch_size
```
This iterates through blockchain data in batches, processes transactions, and writes results to CSV.

## 📦 Dependencies
- 🐍 Python 3
- 📡 `requests` - for API requests
- 🗃 `pandas` - for data handling
- 🔢 `numpy` - for numerical operations
- 📊 `tqdm` - for progress tracking
- 🔗 `base58` - for address conversion
- 🖥 `psutil` - for system resource management

## 📜 License
This project is open-source and available under the MIT License.

## 🤝 Contact
For issues or contributions, please submit a pull request or open an issue on GitHub.

