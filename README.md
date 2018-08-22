<div class="header" align="center">
	<h2>
		<a href="https://github.com/RockyLim92/RockDB_OCSSD_debug" title="(repository-name) temp">
			<img alt="" src="https://github.com/RockyLim92/RocksDB_OCSSD_debug/blob/master/asset/rocky_icon.png" width="100px" height="100px" />
		</a>
		<br />
		RockDB_OCSSD_debug
	</h2>
	<p align="center">:octocat: debug for crc mismatch error on db_bench :octocat:</p>

<!-- Update to dynamic badges -->
</div>


---

### Overview (or Synopsis)
`[Simple Description]`

The cause of the crc mismatch problem is that the size of ***aligned_n*** for reading is smaller than the size required.

To get into details, running db_bench, the mismatch error occuurred when reading in the index block of **59,596bytes(including 5bytes for CRC)**.

The actual offset of index block is ***202488477***.
Now, the code reads ***aligned_n(65536)*** from <em>**aligned\_offset(2024865792)**</em>. So, it cannot cover all index block and cause CRC mismatch problem

The variable ***aligned_n*** sould be set to cover the whole block including CRC 32 bits.


<div class="header" align="center">
	<h2>
		<a href="https://github.com/RockyLim92/RockDB_OCSSD_debug" title="(repository-name) temp">
			<img alt="" src="https://github.com/RockyLim92/RocksDB_OCSSD_debug/blob/master/asset/log.png" width="500px"/>
		</a>
	</h2>
</div>





### Contributor(s)
- **Rocky Lim** - [GitHub](https://github.com/RockyLim92)


### Development
- `[Env]`
- gcc version at least 4.7(for C++11 support)
- gflags
- etc.


### Build (or Installation)
Follow the instructions on [https://github.com/OpenChannelSSD/rocksdb/blob/master/INSTALL.mda]
```
$ cd /nvm/
$ make rocks
```


### Usage  
```
$ cd /nvm
$ sudo source run.sh
```

### Contents
Files Which I modified
- `env_nvm_file.cc`: when allocate variable *alighed_n* in *NvmFile::Read*


### Acknowledgments


### References
- [**rocksdb on OpenChannelSSD**](https://github.com/OpenChannelSSD/rocksdb)
- etc.

