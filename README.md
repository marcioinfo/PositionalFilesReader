# Read Positional Files from a config Files:

Easy two-way conversion between Python dictionaries and fixed-width files.

This module has also proven useful for "debugging" a fixed-width spec -- an invalid configuration reports an error that may not be obvious from reading the spec document.

Requires a 'config' dictonary. See unit tests for full example.


```CONFIG SAMPLE = {
    "Tipo_registro": {
        "required": True,
        "type": "integer",
        "start_pos": 1,
        "end_pos": 1
    },

    "estabelecimento_matriz": {
        "required": True,
        "type": "integer",
        "start_pos": 2,
        "end_pos": 11,
        "length": 10,
    },

    "data_processamento": {
        "required": True,
        "type": "integer",
        "start_pos": 12,
        "end_pos": 19,
        "length": 8,

    },

    "Periodo_inicial": {
        "type": "integer",
        "start_pos": 20,
        "end_pos": 27,
        "length": 8,
        "required": True
    },

    "Periodo_final": {
        "type": "integer",
        "start_pos": 28,
        "end_pos": 35,
        "length": 8,
        "required": True
    },

    "sequencia": {
        "type": "integer",
        "start_pos": 36,
        "end_pos": 42,
        "length": 7,
        "required": True
    },

    "empresa_adquirente": {
        "required": True,
        "type": "string",
        "start_pos": 43,
        "end_pos": 47,
        "length": 5
        },

    "opcao_extrato": {
        "required": True,
        "type": "integer",
        "start_pos": 48,
        "end_pos": 49,
        "length": 2
        },

    "van": {
        "required": True,
        "type": "string",
        "start_pos": 50,
        "end_pos": 50,
        "length": 1
        },

    "caixa_postal": {
        "required": False,
        "type": "string",
        "start_pos": 51,
        "end_pos": 70,
        "length": 20
        },

    "versão_layout": {
        "required": False,
        "type": "integer",
        "start_pos": 71,
        "end_pos": 73,
        "length": 3
        }
}


def test_fw_to_dict():
    """
    Pass in a line and receive dictionary.
    """

    fw_config = deepcopy(layouts.TIPO2CONFIG)

    fw_obj = FixedWidth(fw_config)
    fw_obj.line = ("210274391334190626532930******311000020190626+00000000352340103   R64061                    79398900000000000001600000000000000000000000000000000000000129000454                      00000019177510012466900000010001001 05                              ")

    values = fw_obj.data

    valid = fw_obj.is_valid



    print(values)
    print(valid)


test_fw_to_dict()
```

Notes:

- A field must have a start_pos and either an end_pos or a length. If both an end_pos and a length are provided, they must not conflict.

- A field may not have a default value if it is required.

- Supported types are string, integer, and decimal.

License: BSD