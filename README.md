# Install xmlsec
Fix Failed building wheel for xmlsec

### brew install xmlsec1 pkg-config

## If still error

```
pip install xmlsec
Collecting xmlsec
  Using cached xmlsec-1.3.13.tar.gz (64 kB)
  Installing build dependencies ... done
  Getting requirements to build wheel ... done
  Preparing metadata (pyproject.toml) ... done
Collecting lxml>=3.8
  Using cached lxml-4.9.2-cp38-cp38-macosx_10_15_x86_64.whl (4.7 MB)
Building wheels for collected packages: xmlsec
  Building wheel for xmlsec (pyproject.toml) ... error
  error: subprocess-exited-with-error
  
  × Building wheel for xmlsec (pyproject.toml) did not run successfully.
  │ exit code: 1
  ╰─> [65 lines of output]
      ...
      /private/var/folders/3r/5tl2g0hd1s5892x7v6_l80680000gp/T/pip-install-l82wgx3k/xmlsec_b1821a1b8b0e4f2e9d01654d56c1f442/src/constants.c:304:46: note: expanded from macro 'PYXMLSEC_ADD_NS_CONSTANT'
          tmp = PyUnicode_FromString((const char*)(JOIN(xmlSec, name))); \
                                                   ^
      /private/var/folders/3r/5tl2g0hd1s5892x7v6_l80680000gp/T/pip-install-l82wgx3k/xmlsec_b1821a1b8b0e4f2e9d01654d56c1f442/src/common.h:19:19: note: expanded from macro 'JOIN'
      #define JOIN(X,Y) DO_JOIN1(X,Y)
                        ^
      /private/var/folders/3r/5tl2g0hd1s5892x7v6_l80680000gp/T/pip-install-l82wgx3k/xmlsec_b1821a1b8b0e4f2e9d01654d56c1f442/src/common.h:20:23: note: expanded from macro 'DO_JOIN1'
      #define DO_JOIN1(X,Y) DO_JOIN2(X,Y)
                            ^
      /private/var/folders/3r/5tl2g0hd1s5892x7v6_l80680000gp/T/pip-install-l82wgx3k/xmlsec_b1821a1b8b0e4f2e9d01654d56c1f442/src/common.h:21:23: note: expanded from macro 'DO_JOIN2'
      #define DO_JOIN2(X,Y) X##Y
                            ^
      <scratch space>:60:1: note: expanded from here
      xmlSecSoap11Ns
      ^
      /private/var/folders/3r/5tl2g0hd1s5892x7v6_l80680000gp/T/pip-install-l82wgx3k/xmlsec_b1821a1b8b0e4f2e9d01654d56c1f442/src/constants.c:320:5: error: use of undeclared identifier 'xmlSecSoap12Ns'; did you mean 'xmlSecXPath2Ns'?
          PYXMLSEC_ADD_NS_CONSTANT(Soap12Ns, "SOAP12");
          ^
      /private/var/folders/3r/5tl2g0hd1s5892x7v6_l80680000gp/T/pip-install-l82wgx3k/xmlsec_b1821a1b8b0e4f2e9d01654d56c1f442/src/constants.c:304:46: note: expanded from macro 'PYXMLSEC_ADD_NS_CONSTANT'
          tmp = PyUnicode_FromString((const char*)(JOIN(xmlSec, name))); \
                                                   ^
      /private/var/folders/3r/5tl2g0hd1s5892x7v6_l80680000gp/T/pip-install-l82wgx3k/xmlsec_b1821a1b8b0e4f2e9d01654d56c1f442/src/common.h:19:19: note: expanded from macro 'JOIN'
      #define JOIN(X,Y) DO_JOIN1(X,Y)
                        ^
      /private/var/folders/3r/5tl2g0hd1s5892x7v6_l80680000gp/T/pip-install-l82wgx3k/xmlsec_b1821a1b8b0e4f2e9d01654d56c1f442/src/common.h:20:23: note: expanded from macro 'DO_JOIN1'
      #define DO_JOIN1(X,Y) DO_JOIN2(X,Y)
                            ^
      /private/var/folders/3r/5tl2g0hd1s5892x7v6_l80680000gp/T/pip-install-l82wgx3k/xmlsec_b1821a1b8b0e4f2e9d01654d56c1f442/src/common.h:21:23: note: expanded from macro 'DO_JOIN2'
      #define DO_JOIN2(X,Y) X##Y
                            ^
      <scratch space>:62:1: note: expanded from here
      xmlSecSoap12Ns
      ^
      /usr/local/Cellar/libxmlsec1/1.3.0/include/xmlsec1/xmlsec/strings.h:34:33: note: 'xmlSecXPath2Ns' declared here
      XMLSEC_EXPORT_VAR const xmlChar xmlSecXPath2Ns[];
                                      ^
      2 errors generated.
      error: command '/usr/bin/clang' failed with exit code 1
      [end of output]
  
  note: This error originates from a subprocess, and is likely not a problem with pip.
  ERROR: Failed building wheel for xmlsec
Failed to build xmlsec
ERROR: Could not build wheels for xmlsec, which is required to install pyproject.toml-based projects
```

This issue occurs because of libxmlsec1 version
## Fix
### Remove libxmlsec1 installed
```
> brew uninstall libxmlsec1
Uninstalling /opt/homebrew/Cellar/libxmlsec1/1.3.1_1... (220 files, 7.5MB)
```
### Download the last known good libxmlsec1
```
> export DESIRED_SHA="7f35e6ede954326a10949891af2dba47bbe1fc17"

# ⚠️ this wget call will fail if you haven't exported DESIRED_SHA as in the preceding line
> wget -O /tmp/libxmlsec1.rb "https://raw.githubusercontent.com/Homebrew/homebrew-core/${DESIRED_SHA}/Formula/libxmlsec1.rb"

--2024-02-16 10:49:28--  https://raw.githubusercontent.com/Homebrew/homebrew-core/7f35e6ede954326a10949891af2dba47bbe1fc17/Formula/libxmlsec1.rb
Resolving raw.githubusercontent.com (raw.githubusercontent.com)... 185.199.111.133, 185.199.108.133, 185.199.109.133, ...
Connecting to raw.githubusercontent.com (raw.githubusercontent.com)|185.199.111.133|:443... connected.
HTTP request sent, awaiting response... 200 OK
Length: 2932 (2.9K) [text/plain]
Saving to: ‘/tmp/libxmlsec1.rb’

/tmp/libxmlsec1.rb                          100%[=========================================================================================>]   2.86K  --.-KB/s    in 0s

2024-02-16 10:49:29 (25.9 MB/s) - ‘/tmp/libxmlsec1.rb’ saved [2932/2932]
```
#### Install the local libxmlsec1 formula from /tmp
```
> brew install --formula /tmp/libxmlsec1.rb

==> Fetching libxmlsec1
==> Downloading https://ghcr.io/v2/homebrew/core/libxmlsec1/manifests/1.2.37
Already downloaded: /Users/daniel/Library/Caches/Homebrew/downloads/0cff6c77c178a7b4826e3146309166ec9d19a0a6580d47e5a1ebaf367cd6c7d0--libxmlsec1-1.2.37.bottle_manifest.json
==> Downloading https://ghcr.io/v2/homebrew/core/libxmlsec1/blobs/sha256:26d6ebddf4e97431819583ad699228360886d81786b332084693d0ad34aa2c72
####################################################################################################################################################################### 100.0%
Warning: libxmlsec1 1.3.1_1 is available and more recent than version 1.2.37.
==> Pouring libxmlsec1--1.2.37.arm64_ventura.bottle.tar.gz
🍺  /opt/homebrew/Cellar/libxmlsec1/1.2.37: 221 files, 6MB
==> Running `brew cleanup libxmlsec1`...
Disable this behaviour by setting HOMEBREW_NO_INSTALL_CLEANUP.
Hide these hints with HOMEBREW_NO_ENV_HINTS (see `man brew`).
Removing: /Users/daniel/Library/Caches/Homebrew/libxmlsec1--1.2.37... (1.2MB)
```
