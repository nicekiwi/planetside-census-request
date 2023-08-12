# Planetside Census Request

An API wrapper to request data from the Census API.

## Usage

### Examples

#### CensusRequest with list validation

```ts
import CensusRequest from 'planetside-census-request';
import { NamespaceType } from 'planetside-census-data';

interface ICharacterFaction {
  character_id: string;
  faction_id: number;
}

const api = new CensusRequest(NamespaceType.PC, 's:example')

const getCharacters = async (
  ids: stirng[],
  collection: string = undefined
) => {
  return await api.get<ICharacterFaction[]>({
    uri: 'character',
    params: {
      'character_id': ids.join(','),
      'c:show': ['character_id','faction_id']
    },
    collection
  });
}

const characters = await getCharacters([
  '54200000000000000',
  '54200000000000001'
], 'character_list');

console.log(characters);

// [
//   {
//     character_id: '54200000000000000',
//     faction_id: 1,
//   },
//   {
//     character_id: '54200000000000001',
//     faction_id: 2,
//   }
// ]
```

#### CensusRequest without list validation

```ts
import CensusRequest from 'planetside-census-request';
import { NamespaceType } from 'planetside-census-data';

interface ICharacterFaction {
  character_id: string;
  faction_id: number;
}

const api = new CensusRequest(NamespaceType.PC, 's:example')

const getCharacters = async (
  ids: stirng[],
  collection: string = undefined
) => {
  return await api.get<ICharacterFaction[]>({
    uri: 'character',
    params: {
      'character_id': ids.join(','),
      'c:show': ['character_id','faction_id']
    },
    collection
  });
}

const characters = await getCharacters([
  '54200000000000000',
  '54200000000000001'
]);

console.log(characters);

// {
//    character_list: [
//      {
//        character_id: '54200000000000000',
//        faction_id: 1,
//      },
//      {
//        character_id: '54200000000000001',
//        faction_id: 2,
//      }
//    ],
//    returned: 2
// }
```
