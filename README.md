
## Naming conventions
1) All public types, functions, enums, global variables, and MACROs in a given library should share the same prefix (preferably the file name).
    ```C
        /* audio.c */
        enum {
            AUDIO_BUFFER_STATE_IDLE,
            AUDIO_BUFFER_STATE_BUSY,
        } AudioBufferState;

        typedef struct audio_manager_t{
            //...
        } AudioManager;

        void audio_set_sample_rate(uint32_t sample_rate_Hz){
            //...
        }
    ```

1) Only abbreviate words if the abbreviation is common and obvious.

1) If a variable reflects physical units (milliseconds, seconds, degree C, volts, etc), include the unit name or abbreviation at the end of the vaiable name.
    ```C
        float time_ms;
        uint32_t battery_voltage_mV;
    ```
1) Name casing
    Type | Case
    -----------|------
    Variable             | lower_snake_case
    Function             | lower_snake_case
    Typedef              | CamelCase
    Enum Value           | SHOUTING_SNAKE_CASE 
    Macros               | SHOUTING_SNAKE_CASE
    Function Like Macros | lower_snake_case

1) private (global static) variables and functions prefix with `prv_`. Words prefixed with `_` or `__` have been reserved by recent C standards for possible language expansions. 

## Assignment
1) use `stdint.h` types  wherever possible.

1) float and double values should include a decimal point and atleast 1 decimal place. Floats should be suffixed with `f`.
    ```C
        float my_float = 1.0f;
        double my_double = 2.0;
        float bad_float = 1; //BAD
        double bad_double = 1; //BAD

        if(myfloat < 3.5f){ //GOOD
            //...
        }

        if(my_double < 3.5){ //GOOD
            //...
        }

        if(myfloat < 3.5){ //BAD - UNCLEAR IF COMPILER WILL STORE CONST AS FLOATS OR CONVERT myFloat TO DOUBLE
            //...
        }
    ```

1) Use C99 style struct assignment
    ```C
    typedef struct eg_struct_t{
        uint32_t member_0;
        float    member_1;
        float    member_2[2];
    } EgStruct;

    EgStruct good_assignment = { //GOOD
        .member_0 = 0xdeadbeef,
        .member_2[0] = 1.0f,
    };

    EgStruct bad_assignment = { //BAD
        0xdeadbeef,
        0.0f,
        {1.0f}
    };
    ```

## Misc
1) Ensure all possible cases are covered in switches (a.k.a. explicitly define `default:` case).
2) Avoid using bitfields (the packing order is compiler dependent)