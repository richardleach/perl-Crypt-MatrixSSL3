[![Build Status](https://travis-ci.org/powerman/perl-Crypt-MatrixSSL3.svg?branch=master)](https://travis-ci.org/powerman/perl-Crypt-MatrixSSL3)
[![Coverage Status](https://coveralls.io/repos/powerman/perl-Crypt-MatrixSSL3/badge.svg?branch=master)](https://coveralls.io/r/powerman/perl-Crypt-MatrixSSL3?branch=master)

# NAME

Crypt::MatrixSSL3 - Perl extension for SSL and TLS using MatrixSSL.org v3.7.2b

# VERSION

This document describes Crypt::MatrixSSL3 version v3.7.3

# SYNOPSIS

    use Crypt::MatrixSSL3;

    # 1. See the MatrixSSL documentation.
    # 2. See example scripts included in this package:
    #       ssl_client.pl
    #       ssl_server.pl
    #       functions.pl

# DESCRIPTION

Crypt::MatrixSSL3 lets you use the MatrixSSL crypto library (see
http://matrixssl.org/) from Perl.  With this module, you will be
able to easily write SSL and TLS client and server programs.

MatrixSSL includes everything you need, all in under 50KB.

You will need a "C" compiler to build this, unless you're getting
the ".ppm" prebuilt Win32 version.  Crypt::MatrixSSL3 builds cleanly
on (at least) Windows, Linux, and Macintosh machines.

MatrixSSL is an Open Source (GNU General Public License) product, and is
also available commercially if you need freedom from GNU rules.

Everything you need is included here, but check the MatrixSSL.org
web site to make sure you've got the latest version of the
MatrixSSL "C" code if you like (it's in the directory "./matrixssl"
of this package if you want to replace the included version from
the MatrixSSL.org download site.)

# TERMINOLOGY

When a client establishes an SSL connection without sending a SNI extension in its CLIENT\_HELLO message we say that the client connects to the **default server**.

If a SNI extension is present then the client connects to a **virtual host**.

# EXPORTS

Constants and functions can be exported using different tags.
Use tag ':all' to export everything.

By default (tag ':DEFAULT') only SSL\_MAX\_PLAINTEXT\_LEN and return code
constants (tag ':RC') will be exported.

- :Version

        SSL2_MAJ_VER
        SSL3_MAJ_VER
        SSL3_MIN_VER
        TLS_1_1_MIN_VER
        TLS_1_2_MIN_VER
        TLS_MAJ_VER
        TLS_MIN_VER
        MATRIXSSL_VERSION
        MATRIXSSL_VERSION_MAJOR
        MATRIXSSL_VERSION_MINOR
        MATRIXSSL_VERSION_PATCH
        MATRIXSSL_VERSION_CODE

- :Cipher

    Used in matrixSslSetCipherSuiteEnabledStatus().

        #******************************************************************************
        #
        #   Recommended cipher suites:
        #
        #   Define the following to enable various cipher suites
        #   At least one of these must be defined.  If multiple are defined,
        #   the handshake will determine which is best for the connection.
        #

        TLS_RSA_WITH_AES_128_CBC_SHA
        TLS_RSA_WITH_AES_256_CBC_SHA
        TLS_RSA_WITH_AES_128_CBC_SHA256
        TLS_RSA_WITH_AES_256_CBC_SHA256
        TLS_RSA_WITH_AES_128_GCM_SHA256

        # Pre-Shared Key Ciphers
        TLS_RSA_WITH_AES_256_GCM_SHA384
        TLS_PSK_WITH_AES_256_CBC_SHA
        TLS_PSK_WITH_AES_128_CBC_SHA
        TLS_PSK_WITH_AES_256_CBC_SHA384
        TLS_PSK_WITH_AES_128_CBC_SHA256

        # Ephemeral ECC DH keys, ECC DSA certificates
        TLS_ECDHE_ECDSA_WITH_AES_256_CBC_SHA
        TLS_ECDHE_ECDSA_WITH_AES_128_CBC_SHA
        TLS_ECDHE_ECDSA_WITH_AES_128_CBC_SHA256
        TLS_ECDHE_ECDSA_WITH_AES_256_CBC_SHA384
        TLS_ECDHE_ECDSA_WITH_AES_128_GCM_SHA256
        TLS_ECDHE_ECDSA_WITH_AES_256_GCM_SHA384

        # Ephemeral ECC DH keys, RSA certificates
        TLS_ECDHE_RSA_WITH_AES_256_CBC_SHA
        TLS_ECDHE_RSA_WITH_AES_128_CBC_SHA
        TLS_ECDHE_RSA_WITH_AES_256_CBC_SHA384
        TLS_ECDHE_RSA_WITH_AES_128_CBC_SHA256
        TLS_ECDHE_RSA_WITH_AES_256_GCM_SHA384
        TLS_ECDHE_RSA_WITH_AES_128_GCM_SHA256

        # Non-Ephemeral ECC DH keys, ECC DSA certificates
        TLS_ECDH_ECDSA_WITH_AES_128_CBC_SHA
        TLS_ECDH_ECDSA_WITH_AES_256_CBC_SHA
        TLS_ECDH_ECDSA_WITH_AES_128_CBC_SHA256
        TLS_ECDH_ECDSA_WITH_AES_256_CBC_SHA384
        TLS_ECDH_ECDSA_WITH_AES_128_GCM_SHA256
        TLS_ECDH_ECDSA_WITH_AES_256_GCM_SHA384

        # Non-Ephemeral ECC DH keys, RSA certificates
        TLS_ECDH_RSA_WITH_AES_256_CBC_SHA
        TLS_ECDH_RSA_WITH_AES_128_CBC_SHA
        TLS_ECDH_RSA_WITH_AES_256_CBC_SHA384
        TLS_ECDH_RSA_WITH_AES_128_CBC_SHA256
        TLS_ECDH_RSA_WITH_AES_256_GCM_SHA384
        TLS_ECDH_RSA_WITH_AES_128_GCM_SHA256


        #******************************************************************************
        #
        #   These cipher suites are secure, but not in general use. Enable only if 
        #   specifically required by application.
        #
        TLS_DHE_PSK_WITH_AES_256_CBC_SHA
        TLS_DHE_PSK_WITH_AES_128_CBC_SHA
        TLS_DHE_RSA_WITH_AES_256_CBC_SHA
        TLS_DHE_RSA_WITH_AES_128_CBC_SHA
        TLS_DHE_RSA_WITH_AES_128_CBC_SHA256
        TLS_DHE_RSA_WITH_AES_256_CBC_SHA256


        #******************************************************************************
        #
        #   These cipher suites are generally considered weak, not recommended for use.
        #
        TLS_ECDHE_RSA_WITH_3DES_EDE_CBC_SHA
        SSL_DHE_RSA_WITH_3DES_EDE_CBC_SHA
        SSL_RSA_WITH_3DES_EDE_CBC_SHA
        TLS_RSA_WITH_SEED_CBC_SHA
        SSL_RSA_WITH_RC4_128_SHA
        SSL_RSA_WITH_RC4_128_MD5


        #******************************************************************************
        #
        #   These cipher suites do not combine authentication and encryption and
        #   are not recommended for use-cases that require strong security or 
        #   Man-in-the-Middle protection.
        #
        TLS_DH_anon_WITH_AES_256_CBC_SHA
        TLS_DH_anon_WITH_AES_128_CBC_SHA
        SSL_DH_anon_WITH_3DES_EDE_CBC_SHA
        SSL_DH_anon_WITH_RC4_128_MD5
        SSL_RSA_WITH_NULL_SHA
        SSL_RSA_WITH_NULL_MD5


        # Other
        SSL_NULL_WITH_NULL_NULL
        TLS_RSA_WITH_IDEA_CBC_SHA

    Flag for matrixSslEncodeRehandshake():

        SSL_OPTION_FULL_HANDSHAKE

- :Alert

    Alert level codes:

        SSL_ALERT_LEVEL_FATAL
        SSL_ALERT_LEVEL_WARNING

    Alert description codes:

        SSL_ALERT_ACCESS_DENIED
        SSL_ALERT_BAD_CERTIFICATE
        SSL_ALERT_BAD_RECORD_MAC
        SSL_ALERT_CERTIFICATE_EXPIRED
        SSL_ALERT_CERTIFICATE_REVOKED
        SSL_ALERT_CERTIFICATE_UNKNOWN
        SSL_ALERT_CLOSE_NOTIFY
        SSL_ALERT_DECODE_ERROR
        SSL_ALERT_DECOMPRESSION_FAILURE
        SSL_ALERT_DECRYPTION_FAILED
        SSL_ALERT_DECRYPT_ERROR
        SSL_ALERT_HANDSHAKE_FAILURE
        SSL_ALERT_ILLEGAL_PARAMETER
        SSL_ALERT_INAPPROPRIATE_FALLBACK
        SSL_ALERT_INSUFFICIENT_SECURITY
        SSL_ALERT_INTERNAL_ERROR
        SSL_ALERT_NONE
        SSL_ALERT_NO_APP_PROTOCOL
        SSL_ALERT_NO_CERTIFICATE
        SSL_ALERT_NO_RENEGOTIATION
        SSL_ALERT_PROTOCOL_VERSION
        SSL_ALERT_RECORD_OVERFLOW
        SSL_ALERT_UNEXPECTED_MESSAGE
        SSL_ALERT_UNKNOWN_CA
        SSL_ALERT_UNRECOGNIZED_NAME
        SSL_ALERT_UNSUPPORTED_CERTIFICATE
        SSL_ALERT_UNSUPPORTED_EXTENSION

- :Error

    Error codes from different functions:

        PS_FAILURE
        MATRIXSSL_ERROR
        PS_ARG_FAIL
        PS_CERT_AUTH_FAIL
        PS_CERT_AUTH_FAIL_AUTHKEY
        PS_CERT_AUTH_FAIL_BC
        PS_CERT_AUTH_FAIL_DN
        PS_CERT_AUTH_FAIL_EXTENSION
        PS_CERT_AUTH_FAIL_PATH_LEN
        PS_CERT_AUTH_FAIL_REVOKED
        PS_CERT_AUTH_FAIL_SIG
        PS_DISABLED_FEATURE_FAIL
        PS_EAGAIN
        PS_INTERRUPT_FAIL
        PS_LIMIT_FAIL
        PS_MEM_FAIL
        PS_PARSE_FAIL
        PS_PENDING
        PS_PLATFORM_FAIL
        PS_PROTOCOL_FAIL
        PS_TIMEOUT_FAIL
        PS_UNSUPPORTED_FAIL

- :RC

    Return codes from different functions:

        PS_SUCCESS
        MATRIXSSL_SUCCESS
        MATRIXSSL_APP_DATA
        MATRIXSSL_APP_DATA_COMPRESSED
        MATRIXSSL_HANDSHAKE_COMPLETE
        MATRIXSSL_RECEIVED_ALERT
        MATRIXSSL_REQUEST_CLOSE
        MATRIXSSL_REQUEST_RECV
        MATRIXSSL_REQUEST_SEND

- :Limit

    Max amount of disabled ciphers in matrixSslSetCipherSuiteEnabledStatus():

        SSL_MAX_DISABLED_CIPHERS

    Max size for message in matrixSslEncodeToOutdata():

        SSL_MAX_PLAINTEXT_LEN

- :Validate

    Return code in user validation callback:

        SSL_ALLOW_ANON_CONNECTION

- :Bool

    Booleans used in matrixSslSetCipherSuiteEnabledStatus() and {authStatus}:

        PS_TRUE
        PS_FALSE

- :Func

        set_cipher_suite_enabled_status
        get_ssl_alert
        get_ssl_error

# FUNCTIONS

Some MatrixSSL functions are not accessible from Perl.

These functions will be called automatically before creating first
object of any class (::Keys, ::SessID, ::Client, ::Server or ::HelloExt)
and after last object will be destroyed.

    matrixSslOpen
    matrixSslClose

These functions implement optimization which is useless in Perl:

    matrixSslGetWritebuf
    matrixSslEncodeWritebuf

- **Open**()
- **Close**()

    If you write server intensive applications it is still better to control
    how often the MatrixSSL library gets initialized/deinitialized. For this
    you can call

        Crypt::MatrixSSL3::Open()

    to initialize the library at the start of you application and

        Crypt::MatrixSSL3::Close()

    to deinitialize the library when your application ends.

- **capabilities**()

    Returns a bitwise OR combination of the following constants:

        SHARED_SESSION_CACHE_ENABLED     - shared session cache between multiple processes is enabled
        STATELESS_TICKETS_ENABLED        - stateless ticket session resuming support is enabled
        DH_PARAMS_ENABLED                - loading the DH param for DH cipher suites is enabled
        ALPN_ENABLED                     - Application Layer Protocol Negotiation callback support is enabled
        SNI_ENABLED                      - Server Name Identification (virtual hosts) support is enabled
        OCSP_STAPLES_ENABLED             - handling of the "status_request" TLS extension by responding with an OCSP staple is enabled
        CERTIFICATE_TRANSPARENCY_ENABLED - handling of the "signed_certificate_timestamp" TLS extension is enabled

    Before using any of these features it's a good idea to test if MatrixSSL is supporting them.

- **set\_cipher\_suite\_enabled\_status**( $cipherId, $status )

        matrixSslSetCipherSuiteEnabledStatus( NULL, $cipherId, $status )

    If this function will be used, matrixSslClose() will be never called.

- **get\_ssl\_alert**( $ptBuf )

    Unpack alert level and description from $ptBuf returned by
    $ssl->received\_data() or $ssl->processed\_data().

    Return ($level, $descr) in list context, and $descr in scalar context.
    Both $level and $descr are dualvars (code in numeric context and text
    in string context).

- **get\_ssl\_error**( $rc )

    Return dualvar for this error code (same as $rc in numeric context and
    text error name in string context).

- **refresh\_OCSP\_staple**( $server\_index, $index, $DERfile )

    Used to refresh an already loaded OCSP staple either for a default server or for a virtual host.

    Parameters:

    - $server\_index

        If you want to update the OCSP staple for a virtual host this parameter must have the returned value of the first $sll->init\_SNI(...) call.

        If you want to update the OCSP staple for a default server this parameter must be -1 or undef.

    - $index

        When updating a virtual host ($server\_index > -1) this value specifies the 0-based index of the virtual host for which the OCSP staple should be refreshed.

        When updating a default server this value specifies the index returned by the $ssl->set\_OCSP\_staple(...) first call.

    - $DERfile

        File containing the new OCSP staple in DER format as it was received from the CA's OCSP responder.

    Returns PS\_SUCCESS if the update was successful.

- **refresh\_SCT\_buffer** ( $server\_index, $index, $SCT\_params )

    Used to refresh an already loaded CT extension data buffer either for a default server or for a virtual host.

    Parameters:

    - $server\_index and $index the same as refresh\_OCSP\_staple above, but $indexs take the return value of the first $ssl->set\_SCT\_buffer(...) call
    - $SCT\_params

        Perl scalar contains a file name with prepared extension data.
        Perl array reference with file names of SCT binary structures that the function will use to create the extension data.

    Returns the number of files loaded in order to build extension data.

- **set\_VHIndex\_callback** ( \\&VHIndexCallback )

    More information about &VHIndexCallback in the CALLBACKS section.

# CLASSES

Constructors for all classes will throw exception on error instead of
returning error as matrixSslNew\*() functions do. Exception will be
thrown using ` croak($return_code) `, so to get $return\_code from $@
you should convert it back to number:

    eval { $client = Crypt::MatrixSSL3::Client->new(...) };
    $return_code = 0+$@ if $@;

## Crypt::MatrixSSL3::Keys

- **new**()

        matrixSslNewKeys( $keys )

    Return new object $keys.
    Throw exception if matrixSslNewKeys() doesn't return PS\_SUCCESS.
    When this object will be destroyed will call:

        matrixSslDeleteKeys( $keys )

- $keys->**load\_rsa**( $certFile, $privFile, $privPass, $trustedCAcertFiles )

        matrixSslLoadRsaKeys( $keys, $certFile,
            $privFile, $privPass, $trustedCAcertFiles )

- $keys->**load\_rsa\_mem**( $cert, $priv, $trustedCA )

        matrixSslLoadRsaKeysMem( $keys, $cert, length $cert,
            $priv, length $priv, $trustedCA, length $trustedCA )

- $keys->**load\_pkcs12**( $p12File, $importPass, $macPass, $flags )

        matrixSslLoadPkcs12( $keys, $p12File, $importPass, length $importPass,
            $macPass, length $macPass, $flags )

- $keys->**load\_DH\_params**( $DH\_params\_file )

        matrixSslLoadDhParams ( $keys, $DH_params_file )

- $keys->**load\_session\_ticket\_keys**( $name, $symkey, $hashkey ) `server side`

        matrixSslLoadSessionTicketKeys ($keys, $name, $symkey, length $symkey, $haskkey, length $hashkey )

## Crypt::MatrixSSL3::SessID

- **new**()

    Return new object $sessID representing (sslSessionId\_t\*) type.
    Throw exception if failed to allocate memory.
    When this object will be destroyed will free memory, so you should
    keep this object while there are exist Client/Server session
    which uses this $sessID.

- $sessID->**clear**()

        matrixSslClearSessionId($sessID);

## Crypt::MatrixSSL3::Client

- **new**( $keys, $sessID, \\@cipherSuites, \\&certValidator, $expectedName, $extensions, \\&extensionCback )

        matrixSslNewClientSession( $ssl, $keys, $sessID, \@cipherSuites,
            \&certValidator, $expectedName, $extensions, \&extensionCback )

    Return new object $ssl.
    Throw exception if matrixSslNewClientSession() doesn't return
    MATRIXSSL\_REQUEST\_SEND.
    When this object will be destroyed will call:

        matrixSslDeleteSession( $ssl )

    More information about callbacks &certValidator and &extensionCback
    in next section.

## Crypt::MatrixSSL3::Server

- **new**( $keys, \\&certValidator )

        matrixSslNewServerSession( $ssl, $keys, \&certValidator )

    Return new object $ssl.
    Throw exception if matrixSslNewServerSession() doesn't return PS\_SUCCESS.
    When this object will be destroyed will call:

        matrixSslDeleteSession( $ssl )

    More information about callback &certValidator in next section.

## Crypt::MatrixSSL3::Client and Crypt::MatrixSSL3::Server

- $ssl->**get\_outdata**( $outBuf )

    Unlike C API, it doesn't set $outBuf to memory location inside MatrixSSL,
    but instead it append buffer returned by C API to the end of $outBuf.

        matrixSslGetOutdata( $ssl, $tmpBuf )
        $outBuf .= $tmpBuf

- $ssl->**sent\_data**( $bytes )

        matrixSslSentData( $ssl, $bytes )

- $ssl->**get\_readbuf**( $inBuf )

    Unlike C API, it doesn't set $inBuf to memory location inside MatrixSSL,
    but instead it copy data from beginning of $inBuf into buffer returned by
    C API and cut copied data from beginning of $inBuf (it may copy less bytes
    than $inBuf contain if size of buffer provided by MatrixSSL will be smaller).

        $n = matrixSslGetReadbuf( $ssl, $buf )
        $n = min($n, length $inBuf)
        $buf = substr($inBuf, 0, $n, q{})

    It is safe to call it with empty $inBuf, but this isn't a good idea
    performance-wise.

- $ssl->**received\_data**( $bytes, $ptBuf )

        matrixSslReceivedData( $ssl, $bytes, $ptBuf, $ptLen )

- $ssl->**processed\_data**( $ptBuf )

        matrixSslProcessedData( $ssl, $ptBuf, $ptLen )

    In case matrixSslReceivedData() or matrixSslProcessedData() will return
    MATRIXSSL\_RECEIVED\_ALERT, you can get alert level and description from
    $ptBuf:

        my ($level, $descr) = get_ssl_alert($ptBuf);

- $ssl->**encode\_to\_outdata**( $outBuf )

        matrixSslEncodeToOutdata( $ssl, $outBuf, length $outBuf )

- $ssl->**encode\_closure\_alert**( )

        matrixSslEncodeClosureAlert( $ssl )

- $ssl->**encode\_rehandshake**( $keys, \\&certValidator, $sessionOption, \\@cipherSuites )

        matrixSslEncodeRehandshake( $ssl, $keys, \&certValidator,
            $sessionOption, \@cipherSuites )

    More information about callback &certValidator in next section.

- $ssl->**set\_cipher\_suite\_enabled\_status**( $cipherId, $status )

        matrixSslSetCipherSuiteEnabledStatus( $ssl, $cipherId, $status )

- $anon = $ssl->**get\_anon\_status**()

        matrixSslGetAnonStatus( $ssl, $anon )

- $ssl->**init\_SNI**( $sni\_index, $ssl\_id, $sni\_params ) `server side`

    Used to initialize the virtual host configuration for a server (socket). This function can be called in two ways:

        1) $sni_index = $ssl->init_SNI( -1, $ssl_id, $sni_params ) - one time, after the first client was accepted and the server SSL session created

    When $sni\_index is -1 or undef the XS module will allocate and initialize a SNI server structure using the
    parameters present in $sni\_params. After that, it will register the MatrixSSL SNI callback to an internal XS
    function using the newly created SNI server structure as parameter.
    This MUST be called only once per server socket and the result $sni\_index value must be cached for subsequent calls.

        2) $ssl->init_SNI( $sni_index, $ssl_id ) - many times, after clients are accepted and server SSL sessions created

    This will skip the SNI server initialization part and just register the MatrixSSL SNI callback to an internal XS
    function using the SNI server structure specified by $sni\_index as parameter.

    Parameters:

    - $sni\_index int >= 0 or -1|undef

        For the first call this parameter MUST be -1. Subsequent calls MUST use the returned value of the first call.

    - $sni\_params \[\[...\],...\] or undef

        This is a reference to an array that contains one or more array references:

            $sni_params = [                                      # virtual hosts support - when a client sends a TLS SNI extension, the settings below will apply
                                                                 #                         based on the requested hostname
                # virtual host 0 (also referred in the code as SNI entry 0)
                [
                    'hostname',                                  # regular expression for matching the hostname
                    '/path/to/certificate;/path/to/CA-chain',    # KEY - certificate (the CA-chain is optional)
                    '/path/to/private_key',                      # KEY - private key
                    '/path/to/DH_params',                        # KEY - file containing the DH parameter used with DH ciphers
                    '1234567890123456',                          # KEY - TLS session tickets - 16 bytes unique identifier
                    '12345678901234567890123456789012',          # KEY - TLS session tickets - 128/256 bit encryption key
                    '12345678901234567890123456789012',          # KEY - TLS session tickets - 256 bit hash key
                    '/path/to/OCSP_staple.der',                  # SESSION - file containing a OCSP staple that gets sent when a client
                                                                 #           send a TLS status request extension
                    [                                            # SESSION - Certificate Transparency SCT files used to build the 'signed_certificate_timestamp' TLS extension data buffer
                        '/path/to/SCT1.sct',
                        '/path/to/SCT2.sct',
                        ...
                    ]
                    # instead of the Certificate Transparency SCT files you can specify a scalar with a single file that contains multiple SCT files
                    # note that this file is not just a concatenation of the SCT files, but a ready-to-use 'signed_certificate_timestamp' TLS extension data buffer
                    # see ct-submit.pl for more info
                    #'/path/to/CT_extension_data_buffer
                ],
                # virtual host 1
                ...
            ]

    - $ssl\_id

        A 32 bit integer that uniquely identifies this session. This parameter will be sent back when MatrixSSL calls the SNI callback defined in the XS module when a client sends a SNI extension.
        If the XS module is able to match the requested client hostname it will call the Perl callback set with set\_VHIndex\_callback.

    Returns the index of the internal SNI server structure used for registering the MatrixSSL SNI callback. This MUST be saved after the first call.

- $ssl->**set\_OCSP\_staple**( $ocsp\_index, $DERfile ) `server side`

    Used to set the OCSP staple to be returned if the client sends the "status\_request" TLS extension. Note that this function call
    only affects the **default server**. Virtual hosts are managed by using the $ssl->init\_SNI(...)

    See $ssl->init\_SNI(...) for usage.

    The $DERfile parameter specifies the file containing the OCSP staple in DER format.

- $ssl->**load\_OCSP\_staple**( $DERfile ) `server side`

    Loads an OCSP staple to be returned if the client sends the "status\_request" TLS extension.

    Note that this function is very inefficient because the loaded data is bound to the specified session and it will be freed when the session is destroyed.
    It has the advantage that the session will contain the latest OCSP data if the OCSP DER file is refreshed in the meantime.

    Don't be lazy and use $ssl->set\_OCSP\_staple and refresh\_OCSP\_staple instead.

- $ssl->**set\_SCT\_buffer**( $sct\_index, $SCT\_params ) `server side`

    Used to set the extension data to be returned if the client sends the "signed\_certificate\_timestamp" TLS extension. Note that this function call
    only affects the **default server**. Virtual hosts are managed by using the $ssl->init\_SNI(...)

    See $ssl->init\_SNI(...) for usage.

    The $SCT\_params has the same structure as the one used in the $ssl->init\_SNI(...) function.

- $ssl->**set\_ALPN\_callback**( \\&ALPNcb ) `server side`

    Sets a callback that will receive as parameter data sent by the client in the ALPN TLS extension.

    More information about callback &ALPNcb in next section.

## Crypt::MatrixSSL3::HelloExt

- **new**( )

        matrixSslNewHelloExtension>( $extension )

    Return new object $extension.
    Throw exception if matrixSslNewHelloExtension() doesn't return PS\_SUCCESS.
    When this object will be destroyed will call:

        matrixSslDeleteHelloExtension( $extension )

- $extension->**load**( $ext, $extType )

        matrixSslLoadHelloExtension( $extension, $ext, length $ext, $extType )

# CALLBACKS

- &certValidator

    Will be called with two scalar params: $certInfo and $alert
    (unlike C callback which also have $ssl param).

    Param $certInfo instead of (psX509Cert\_t \*) will contain reference to
    array with certificates. Each certificate will be hash in this format:

        notBefore       => $notBefore,
        notAfter        => $notAfter,
        subjectAltName  => {
            dns             => $dns,
            uri             => $uri,
            email           => $email,
        },
        subject        => {
            country         => $country,
            state           => $state,
            locality        => $locality,
            organization    => $organization,
            orgUnit         => $orgUnit,
            commonName      => $commonName,
        },
        issuer         => {
            country         => $country,
            state           => $state,
            locality        => $locality,
            organization    => $organization,
            orgUnit         => $orgUnit,
            commonName      => $commonName,
        },
        authStatus     => $authStatus,

    This callback must return single scalar with integer value (as described in
    MatrixSSL documentation). If callback die(), then warning will be printed,
    and execution will continue assuming callback returned -1.

- &extensionCback

    Will be called with two scalar params: $type and $data
    (unlike C callback which also have $ssl and length($data) params).

    This callback must return single scalar with integer value (as described in
    MatrixSSL documentation). If callback die(), then warning will be printed,
    and execution will continue assuming callback returned -1.

- &ALPNcb

    Will be called with an array reference containing strings with the protocols
    the client supports.

    The callback must return the 0-based index of a supported protocol or
    \-1 if none of the client supplied protocols is supported.

- &VHIndexCallback

    Will be called whenever we have a successful match against the hostname specified by the client in its SNI extension.
    This will inform the Perl code which virtual host the current SSL session belongs to.

    Will be called with 2 parameters:

        $ssl_id - this is the $ssl_id used in the $ssl->init_SNI(...) function call
        $index - a 0-based int specifying which virtual host matchd the client requested hostname

    Doesn't return anything.

# SEE ALSO

http://www.MatrixSSL.org - the download from this site includes
simple yet comprehensive documentation in PDF format.

# SUPPORT

## Bugs / Feature Requests

Please report any bugs or feature requests through the issue tracker
at [https://github.com/powerman/perl-Crypt-MatrixSSL3/issues](https://github.com/powerman/perl-Crypt-MatrixSSL3/issues).
You will be notified automatically of any progress on your issue.

## Source Code

This is open source software. The code repository is available for
public review and contribution under the terms of the license.
Feel free to fork the repository and submit pull requests.

[https://github.com/powerman/perl-Crypt-MatrixSSL3](https://github.com/powerman/perl-Crypt-MatrixSSL3)

    git clone https://github.com/powerman/perl-Crypt-MatrixSSL3.git

## Resources

- MetaCPAN Search

    [https://metacpan.org/search?q=Crypt-MatrixSSL3](https://metacpan.org/search?q=Crypt-MatrixSSL3)

- CPAN Ratings

    [http://cpanratings.perl.org/dist/Crypt-MatrixSSL3](http://cpanratings.perl.org/dist/Crypt-MatrixSSL3)

- AnnoCPAN: Annotated CPAN documentation

    [http://annocpan.org/dist/Crypt-MatrixSSL3](http://annocpan.org/dist/Crypt-MatrixSSL3)

- CPAN Testers Matrix

    [http://matrix.cpantesters.org/?dist=Crypt-MatrixSSL3](http://matrix.cpantesters.org/?dist=Crypt-MatrixSSL3)

- CPANTS: A CPAN Testing Service (Kwalitee)

    [http://cpants.cpanauthors.org/dist/Crypt-MatrixSSL3](http://cpants.cpanauthors.org/dist/Crypt-MatrixSSL3)

# AUTHORS

C. N. Drake &lt;christopher@pobox.com>

Alex Efros &lt;powerman@cpan.org>

# COPYRIGHT AND LICENSE

This software is Copyright (c) 2005- by C. N. Drake &lt;christopher@pobox.com>.

This software is Copyright (c) 2012- by Alex Efros &lt;powerman@cpan.org>.

This is free software, licensed under:

    The GNU General Public License version 2

MatrixSSL is distributed under the GNU General Public License,
Crypt::MatrixSSL3 uses MatrixSSL, and so inherits the same license.