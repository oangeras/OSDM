# Mocking the OSDM Interface

## Scenario 1: Basel SBB - Landquart

Mocked resources:

- GET `/locations/?matchValue=Basel`
- GET `/locations/?matchValue=Klosters`
- GET `/locations/?matchValue=Küblis`
- GET `/locations/?matchValue=Landquart`
- GET `/locations/?matchValue=Sargans`
- GET `/locations/?matchValue=Schiers`
- GET `/locations/?matchValue=Zürich`
- GET `/trips/
- POST `/trips-collection`:
  - `tripSearch.origin.code=` and `tripSearch.destination.code=`
  - `tripSearch.origin.code=` and `tripSearch.destination.code=`
- POST `/trip-offers-collection`
- POST `/bookings`
- POST `/bookings/{bookingId}/fulfillments`
- GET `/bookings/booking_001/passengers/passenger_001`
- GET `/products/CH00125FIRST`
- GET `/products/CH10125FIRST`
- GET `/fulfillments/94a4c484-702f-11eb-9439-0242ac130002`
- GET `/fulfillments/3730e668-7032-11eb-9439-0242ac130002`
- GET `/fulfillments/406e9432-7032-11eb-9439-0242ac130002`

The [WireMock](https://wiremock.org) is used to build the mock which is configured
by [WireMock Mappings](./mappings/sale-core-mappings.json).

Use `./startMock.sh` to run mock which will run on [https://localhost:8080](https://localhost:8080).

To query the mocked interface a [Postman Collection](OSDM-API.postman_collection.json) is
provided. Additionally, [Postman Environnement](OSDM-API.postman_collection.json) is used to
configure the [Postman](https://www.postman.com) environnement.

## Ids Used for Scenario 1

Ids used for this scenario (`grep -C 2 -n '"id' trip-offer-response-Basel-Klosters.json`):

- stops: Basel SBB, Klosters Platz, Küblis, Landquart, Sargans, Schiers, Zürich HB.
- trips:
  - `50898cd4-0d1e-4456-92bd-c119d419728e` (Trip Basel SBB - Landquart, 2021-03-22 13:08)
  - `6db18e19-d87f-442b-b80c-90e3b7007f20` (Trip Landquart - Klosters, 2021-03-22 15:20)
  - `3fa85f64-5717-4562-b3fc-2c963f66afa6` (Trips Collection - Basel SBB - Klosters Platz, 2021-03-22 13:08)
- trip offer id:  `tripOffer_001`
- admission id: `admission_BaselSBB-Klosters`
- reservation ids:
  - `reservation_BaselSBB-Landquart`
  - `reservation_Landquart-Klosters`
- product ids:
  - `CH00125FIRST`
  - `CH10125FIRST`
- passenger id: `ca622d56-7033-11eb-9439-0242ac130002`
- fulfillment Id:
  - `94a4c484-702f-11eb-9439-0242ac130002` (Admission Basel SBB - Davos Platz)
  - `3730e668-7032-11eb-9439-0242ac130002` (Reservation Basel SBB - Landquart)
  - `406e9432-7032-11eb-9439-0242ac130002` (Reservation Landquart - Davos Platz)

## Journeys to Add Next

- Zürich Hb - Wien (öBB)
- Basel SBB - Frankfurt (DB)
- Basel SBB - Paris (SNCF)
- Zürich HB - Milano (Trenitalia)
- Paris - London (Sqills)
- London - Edinburgh (Silverrail)
- Paris - Brüssels (BENE)
- Paris - Bordeaux (Amadeus)
- Bordeaux - Barcelona (Trainline)
- Barcelona - Madrid (Renfe)
- ...