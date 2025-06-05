# LeakGenerator v2.0

[![License](https://img.shields.io/badge/license-MIT-blue.svg)](https://en.wikipedia.org/wiki/MIT_License) [![python](https://img.shields.io/badge/Python-3.9%20%7C%203.10%20%7C%203.11%20%7C%203.12-blue.svg)](https://www.python.org/downloads/)

## Idea

Generate realistic-looking email and password leak databases for testing, research, and fun.

Want to create 280 million fake leaked credentials that look like they came from a real breach? Need a MySQL dump of "compromised" users for security training? This script got you covered.

## Why?

For testing leak detection systems, password analysis tools, security training, or just for fun. Remember that massive "leak" that wasn't? http://arstechnica.co.uk/security/2016/05/the-massive-password-breach-that-wasnt-google-says-data-is-98-bogus/

Now you can make your own!

## Features

- **Multiple Output Formats**: TXT, CSV, JSON, MySQL, MSSQL, PostgreSQL dumps
- **Realistic Data Generation**: Weighted patterns for emails and passwords that mirror real leaks
- **20+ Hash Types**: MD5, SHA1/256/512, NTLM, bcrypt*, scrypt*, Argon2*, and salted variants
- **Flexible Output**: Include or exclude passwords with `--no-password`
- **High Performance**: Multi-threaded generation with progress tracking
- **No Dependencies**: Core features work with standard Python (bcrypt/scrypt/argon2 optional)

## Installation

```bash
git clone https://github.com/op7ic/LeakGenerator
cd LeakGenerator

# Optional: Install additional hash libraries
pip install bcrypt scrypt argon2-cffi
```

## Usage

```bash
python leakgen.py -t <hash_type> -m <count> [-f <format>] [-o <output>] [options]
```

### Examples

**Generate 1 million MD5 hashes as MySQL dump:**
```bash
python leakgen.py -t md5 -m 1000000 -f mysql -o leaked_users.sql
```

**Create CSV with SHA256 hashes (no passwords):**
```bash
python leakgen.py -t sha256 -m 50000 -f csv --no-password -o hashes.csv
```

**Generate realistic JSON credentials:**
```bash
python leakgen.py -t clear -m 10000 -f json -o credentials.json
```

**Create PostgreSQL dump with bcrypt:**
```bash
python leakgen.py -t bcrypt -m 5000 -f postgres -o secure_leak.sql --table compromised_users
```

**Classic text format (like original):**
```bash
python leakgen.py -t md5_r_salt -m 0x00FFFFFF -o massive_leak.txt
```

### Supported Hash Types

**Basic Hashes** (email:password:hash):
- `md5`, `sha1`, `sha256`, `sha512`, `ntlm`
- `bcrypt`*, `scrypt`*, `argon2`* (*requires additional libraries)

**Salted Hashes** (email:password+salt:hash):
- `md5_r_salt`, `sha1_r_salt`, `sha256_r_salt`, `sha512_r_salt`, `ntlm_r_salt`

**Hash Only** (just the hash):
- `md5_hashonly`, `sha1_hashonly`, `sha256_hashonly`, `sha512_hashonly`, `ntlm_only`

**Special Formats**:
- `clear` - Plain email:password pairs
- `ad_compromise` - Active Directory format (SID:LM:NTLM)

### Output Formats

- **txt** - Classic `email:password:hash` format
- **csv** - Comma-separated with headers
- **json** - JSON array of objects
- **mysql** - MySQL dump with CREATE TABLE
- **mssql** - MSSQL dump with T-SQL syntax
- **postgres** - PostgreSQL dump format

### Options

```
-t, --type        Hash type to generate (required)
-m, --max         Number of entries (supports hex: 0x00FFFFFF)
-f, --format      Output format (default: txt)
-o, --output      Output file (default: stdout)
-j, --threads     Number of threads (default: 1)
--no-password     Exclude passwords from output
--table          Table name for SQL formats (default: users)
```

## What's New in v2.0

- **Realistic Data**: Weighted email patterns (firstname.lastname, nicknames, birth years)
- **Smart Passwords**: Common passwords, year patterns, special characters
- **SQL Dumps**: Direct MySQL/MSSQL/PostgreSQL import ready
- **Flexible Output**: Choose what to include/exclude
- **Better Performance**: Multi-threading and progress tracking
- **More Hash Types**: Added bcrypt, scrypt, and Argon2 support

## Output Examples

**MySQL Dump:**
```sql
INSERT INTO `users` (`email`, `password`, `hash`) VALUES
('john.smith@gmail.com', 'Password2024!', '5994471abb01112afcc18159f6cc74b4f511b99806da59b3caf'),
('sarah_jones1985@yahoo.com', 'love4ever', 'e10adc3949ba59abbe56e057f20f883e');
```

**CSV Format:**
```csv
email,password,hash
alice.johnson@outlook.com,dragon123,482c811da5d5b4bc6d497ffa98491e38
mike99@gmail.com,qwerty2023,a384b6463fc216a5f8ecb6670f86456a
```

**JSON Format:**
```json
[
  {
    "email": "techguru@company.com",
    "password": "Secure123!",
    "hash": "$2b$04$L3qR7Kn7R8yF9N2hFpqFOuG6Y3tZ8nK5jM9pL2wX4vC1sD0eA3hB2"
  }
]
```

## Performance

On a modern system:
- **MD5/SHA**: ~50,000-100,000 entries/second
- **bcrypt**: ~1,000 entries/second (intentionally slow)
- **With threading**: Near-linear speedup with `-j` option

## License

MIT License - see LICENSE file

## Disclaimer

THIS SOFTWARE IS PROVIDED "AS IS", WITHOUT WARRANTY OF ANY KIND, EXPRESS OR IMPLIED, INCLUDING BUT NOT LIMITED TO THE WARRANTIES OF MERCHANTABILITY, FITNESS FOR A PARTICULAR PURPOSE AND NONINFRINGEMENT. IN NO EVENT SHALL THE AUTHORS OR COPYRIGHT HOLDERS BE LIABLE FOR ANY CLAIM, DAMAGES OR OTHER LIABILITY, WHETHER IN AN ACTION OF CONTRACT, TORT OR OTHERWISE, ARISING FROM, OUT OF OR IN CONNECTION WITH THE SOFTWARE OR THE USE OR OTHER DEALINGS IN THE SOFTWARE.