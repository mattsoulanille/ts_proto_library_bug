# ts_proto_library_bug

## Reproducing the Bug
`yarn install`
`yarn build`

Then, if you check `bazel-out/k8-fastbuild/bin/src/house_pb.d.ts`, you'll see the following TypeScript declaration file.
The bug is that the room proto's type is imported as `src_room_pb` but `getKitchen()` returns the type `src_room_pbRoom`,
which has no definition and is the incorrect return type.

```typescript
import * as jspb from "google-protobuf"

import * as src_room_pb from '../src/room_pb';

export class House extends jspb.Message {
  getKitchen(): src_room_pbRoom | undefined;
  setKitchen(value?: src_room_pbRoom): void;
  hasKitchen(): boolean;
  clearKitchen(): void;

  serializeBinary(): Uint8Array;
  toObject(includeInstance?: boolean): House.AsObject;
  static toObject(includeInstance: boolean, msg: House): House.AsObject;
  static serializeBinaryToWriter(message: House, writer: jspb.BinaryWriter): void;
  static deserializeBinary(bytes: Uint8Array): House;
  static deserializeBinaryFromReader(message: House, reader: jspb.BinaryReader): House;
}

export namespace House {
  export type AsObject = {
    kitchen?: src_room_pbRoom.AsObject,
  }
}
```
